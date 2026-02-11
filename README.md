<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Professional Resume Builder</title>

<script src="https://cdn.tailwindcss.com"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>

<style>
.a4{
  width:210mm;
  min-height:297mm;
  background:white;
}
.input{
  width:100%;
  padding:8px;
  border:1px solid #ccc;
  border-radius:6px;
}
</style>
</head>

<body class="bg-gray-100">

<!-- NAV -->
<div class="bg-blue-700 text-white p-4 flex justify-between items-center">
<h1 class="font-bold text-xl">📄 Pro Resume Builder</h1>
<button onclick="downloadPDF()" class="bg-green-500 px-4 py-2 rounded">
Download PDF
</button>
</div>

<div class="flex flex-col md:flex-row gap-6 p-6">

<!-- ================= FORM ================= -->
<div class="w-full md:w-1/3 bg-white p-4 rounded shadow space-y-3 overflow-y-auto max-h-screen">

<h2 class="font-bold">Basic Info</h2>

<input id="photo" type="file" accept="image/*" class="input" onchange="previewPhoto(event)">

<input id="name" placeholder="Full Name" class="input" oninput="update()">
<input id="job" placeholder="Job Title" class="input" oninput="update()">
<input id="phone" placeholder="Phone" class="input" oninput="update()">
<input id="email" placeholder="Email" class="input" oninput="update()">
<input id="link" placeholder="LinkedIn / Portfolio" class="input" oninput="update()">

<textarea id="summary" placeholder="Professional Summary" class="input h-20" oninput="update()"></textarea>

<h2 class="font-bold">Skills (comma separated)</h2>
<input id="skills" placeholder="HTML, CSS, JS, Canva" class="input" oninput="update()">

<!-- Experience -->
<h2 class="font-bold">Experience</h2>
<div id="expContainer"></div>
<button onclick="addExperience()" class="bg-blue-500 text-white px-2 py-1 rounded">
+ Add Experience
</button>

<!-- Education -->
<h2 class="font-bold mt-3">Education</h2>
<div id="eduContainer"></div>
<button onclick="addEducation()" class="bg-blue-500 text-white px-2 py-1 rounded">
+ Add Education
</button>

</div>

<!-- ================= RESUME ================= -->
<div class="flex-1 flex justify-center">
<div id="resume" class="a4 p-10 shadow">

<!-- Header -->
<div class="flex gap-6 items-center mb-6">
<img id="pPhoto" class="w-28 h-28 rounded-full object-cover border hidden">
<div>
<h1 id="pname" class="text-3xl font-bold">Your Name</h1>
<p id="pjob" class="text-blue-600"></p>
<p id="pcontact" class="text-sm"></p>
</div>
</div>

<!-- Summary -->
<h2 class="font-bold border-b mb-1">Profile</h2>
<p id="psummary" class="mb-4 text-sm"></p>

<!-- Skills -->
<h2 class="font-bold border-b mb-1">Skills</h2>
<div id="pskills" class="mb-4 text-sm flex flex-wrap"></div>

<!-- Experience -->
<h2 class="font-bold border-b mb-1">Experience</h2>
<div id="pexp" class="mb-4 text-sm"></div>

<!-- Education -->
<h2 class="font-bold border-b mb-1">Education</h2>
<div id="pedu" class="text-sm"></div>

</div>
</div>
</div>

<script>
let expCount = 0
let eduCount = 0

function previewPhoto(e){
const reader = new FileReader()
reader.onload = function(){
pPhoto.src = reader.result
pPhoto.classList.remove("hidden")
}
reader.readAsDataURL(e.target.files[0])
}

function update(){
pname.innerText = name.value
pjob.innerText = job.value
pcontact.innerText = phone.value+" | "+email.value+" | "+link.value
psummary.innerText = summary.value

pskills.innerHTML = skills.value.split(',')
.map(s=>`<span class="bg-gray-200 px-2 py-1 m-1 rounded">${s.trim()}</span>`).join('')

updateExperience()
updateEducation()
}

function addExperience(){
expCount++
const div = document.createElement("div")
div.innerHTML=`
<input placeholder="Role" class="input mt-1 expRole" oninput="update()">
<input placeholder="Company" class="input mt-1 expCompany" oninput="update()">
<textarea placeholder="Description" class="input mt-1 expDesc" oninput="update()"></textarea>
`
expContainer.appendChild(div)
}

function addEducation(){
eduCount++
const div = document.createElement("div")
div.innerHTML=`
<input placeholder="Degree" class="input mt-1 eduDegree" oninput="update()">
<input placeholder="College" class="input mt-1 eduCollege" oninput="update()">
`
eduContainer.appendChild(div)
}

function updateExperience(){
const roles=document.querySelectorAll(".expRole")
const companies=document.querySelectorAll(".expCompany")
const descs=document.querySelectorAll(".expDesc")

let html=""
for(let i=0;i<roles.length;i++){
html+=`<p><b>${roles[i].value}</b> - ${companies[i].value}<br>${descs[i].value}</p><br>`
}
pexp.innerHTML=html
}

function updateEducation(){
const deg=document.querySelectorAll(".eduDegree")
const col=document.querySelectorAll(".eduCollege")

let html=""
for(let i=0;i<deg.length;i++){
html+=`<p><b>${deg[i].value}</b><br>${col[i].value}</p><br>`
}
pedu.innerHTML=html
}

function downloadPDF(){
html2pdf().from(resume).save("resume.pdf")
}

addExperience()
addEducation()
</script>

</body>
</html>
