<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Smart Resume Builder - Free Tool</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
    <style>
        .a4-page {
            width: 210mm;
            min-height: 297mm;
            background: white;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        @media (max-width: 768px) {
            .a4-page { width: 100%; min-height: auto; }
        }
    </style>
</head>
<body class="bg-gray-100 font-sans">

    <nav class="bg-blue-600 p-4 text-white shadow-lg">
        <div class="container mx-auto flex justify-between items-center">
            <h1 class="text-2xl font-bold">📄 Smart Resume Builder</h1>
            <button onclick="downloadPDF()" class="bg-green-500 hover:bg-green-600 px-4 py-2 rounded font-bold shadow">
                Download PDF
            </button>
        </div>
    </nav>

    <div class="container mx-auto mt-8 p-4 flex flex-col md:flex-row gap-8">
        
        <div class="w-full md:w-1/3 bg-white p-6 rounded-lg shadow-md h-fit">
            <h2 class="text-xl font-bold mb-4 text-gray-700">✏️ Enter Your Details</h2>
            
            <div class="space-y-3 mb-6">
                <input type="text" id="nameInput" placeholder="Full Name" class="w-full p-2 border rounded" oninput="updateResume()">
                <input type="text" id="jobTitleInput" placeholder="Job Title (e.g. Web Developer)" class="w-full p-2 border rounded" oninput="updateResume()">
                <input type="text" id="phoneInput" placeholder="Phone Number" class="w-full p-2 border rounded" oninput="updateResume()">
                <input type="email" id="emailInput" placeholder="Email Address" class="w-full p-2 border rounded" oninput="updateResume()">
                <input type="text" id="linkedinInput" placeholder="LinkedIn / Portfolio URL" class="w-full p-2 border rounded" oninput="updateResume()">
            </div>

            <div class="mb-6">
                <textarea id="summaryInput" placeholder="Professional Summary..." class="w-full p-2 border rounded h-24" oninput="updateResume()"></textarea>
            </div>

            <div class="mb-6">
                <input type="text" id="skillsInput" placeholder="Skills (comma separated)" class="w-full p-2 border rounded" oninput="updateResume()">
                <p class="text-xs text-gray-500">e.g. HTML, CSS, Marketing, Excel</p>
            </div>

            <div class="bg-yellow-100 border border-yellow-300 p-4 rounded text-center text-sm text-yellow-800">
                <strong>Start Your Career!</strong><br>
                <a href="#" class="underline">Get Certified Course Here (Affiliate Link)</a>
            </div>
        </div>

        <div class="w-full md:w-2/3 flex justify-center">
            <div id="resume-preview" class="a4-page p-8 md:p-12 text-gray-800">
                
                <div class="border-b-2 border-gray-800 pb-4 mb-6">
                    <h1 id="previewName" class="text-4xl font-bold uppercase text-gray-900">Your Name</h1>
                    <p id="previewJob" class="text-xl text-blue-600 font-medium mt-1">Job Title</p>
                    <div class="flex flex-wrap gap-4 text-sm mt-3 text-gray-600">
                        <span id="previewPhone">📞 Phone</span>
                        <span id="previewEmail">📧 Email</span>
                        <span id="previewLinkedin">🌐 Portfolio</span>
                    </div>
                </div>

                <div class="mb-6">
                    <h3 class="text-lg font-bold border-b border-gray-300 mb-2 uppercase text-gray-700">Profile</h3>
                    <p id="previewSummary" class="text-sm leading-relaxed text-gray-600">
                        Your professional summary will appear here. Start typing in the form to see changes instantly.
                    </p>
                </div>

                <div class="mb-6">
                    <h3 class="text-lg font-bold border-b border-gray-300 mb-2 uppercase text-gray-700">Skills</h3>
                    <div id="previewSkills" class="flex flex-wrap gap-2">
                        <span class="bg-gray-200 px-2 py-1 text-xs rounded">Your Skills</span>
                    </div>
                </div>

                <div class="mb-6">
                    <h3 class="text-lg font-bold border-b border-gray-300 mb-2 uppercase text-gray-700">Experience</h3>
                    <div class="mb-4">
                        <h4 class="font-bold">Job Position</h4>
                        <p class="text-xs text-gray-500">Company Name | 2020 - Present</p>
                        <ul class="list-disc list-inside text-sm text-gray-600 mt-1">
                            <li>Describe your responsibility here.</li>
                            <li>Mention your achievements.</li>
                        </ul>
                    </div>
                </div>

                <div>
                    <h3 class="text-lg font-bold border-b border-gray-300 mb-2 uppercase text-gray-700">Education</h3>
                    <div>
                        <h4 class="font-bold">Degree / Course Name</h4>
                        <p class="text-xs text-gray-500">University Name | Passing Year</p>
                    </div>
                </div>

            </div>
        </div>
    </div>

    <footer class="bg-gray-800 text-white text-center p-4 mt-12">
        <p>&copy; 2024 Smart Resume Builder. All rights reserved.</p>
    </footer>

    <script>
        function updateResume() {
            // Get Values
            document.getElementById('previewName').innerText = document.getElementById('nameInput').value || "YOUR NAME";
            document.getElementById('previewJob').innerText = document.getElementById('jobTitleInput').value || "Job Title";
            document.getElementById('previewPhone').innerText = "📞 " + (document.getElementById('phoneInput').value || "Phone");
            document.getElementById('previewEmail').innerText = "📧 " + (document.getElementById('emailInput').value || "Email");
            document.getElementById('previewLinkedin').innerText = "🌐 " + (document.getElementById('linkedinInput').value || "Link");
            document.getElementById('previewSummary').innerText = document.getElementById('summaryInput').value || "Your summary goes here...";

            // Handle Skills
            const skillsText = document.getElementById('skillsInput').value;
            const skillsContainer = document.getElementById('previewSkills');
            skillsContainer.innerHTML = ''; // Clear old
            if (skillsText) {
                skillsText.split(',').forEach(skill => {
                    if (skill.trim()) {
                        const span = document.createElement('span');
                        span.className = 'bg-gray-200 px-2 py-1 text-xs rounded text-gray-700 font-medium';
                        span.innerText = skill.trim();
                        skillsContainer.appendChild(span);
                    }
                });
            } else {
                 skillsContainer.innerHTML = '<span class="bg-gray-200 px-2 py-1 text-xs rounded">Skill 1</span>';
            }
        }

        function downloadPDF() {
            const element = document.getElementById('resume-preview');
            const opt = {
                margin:       0,
                filename:     'my-resume.pdf',
                image:        { type: 'jpeg', quality: 0.98 },
                html2canvas:  { scale: 2 },
                jsPDF:        { unit: 'mm', format: 'a4', orientation: 'portrait' }
            };
            html2pdf().set(opt).from(element).save();
        }
    </script>
</body>
</html>
