<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive CV - Mohamed Othman</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <!-- Chosen Palette: Warm Neutral Tones -->
    <!-- Application Structure Plan: The application is designed as a single-page portfolio with a top navigation bar for easy access to key sections. The structure is thematic: an introduction (Hero), a chronological career journey (Timeline), a data-driven skills dashboard (Expertise), and credentials (Education/Certs). This structure was chosen to guide a recruiter through a narrative of professional growth, moving from a high-level summary to detailed experience and specific skills, which is more engaging and intuitive than a traditional, static CV layout. Interactions like the clickable timeline focus on progressive disclosure of information, keeping the UI clean while allowing for deep dives. -->
    <!-- Visualization & Content Choices: 
        - Career Experience -> Goal: Show change, organize info -> Viz: Interactive Vertical Timeline -> Interaction: Click to expand details -> Justification: Visualizes career progression clearly and hides lengthy descriptions by default to reduce clutter. (HTML/CSS/JS).
        - Core Skills -> Goal: Compare, inform -> Viz: Horizontal Bar Chart -> Interaction: Hover for tooltips -> Justification: Provides a quick, scannable visual comparison of key competency areas, which is more impactful than a simple list. (Chart.js/Canvas).
        - Technical Tools -> Goal: Inform -> Viz: Grid of styled cards -> Interaction: None -> Justification: A clean, modern way to display a list of technologies. (HTML/CSS).
        - All other text -> Goal: Inform -> Viz: Styled text blocks and cards -> Interaction: None -> Justification: Ensures readability and professional presentation. (HTML/CSS).
    -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f4f4f5; 
            color: #3f3f46;
        }
        .timeline-item-content {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.5s ease-in-out, padding 0.5s ease-in-out;
            padding-top: 0;
            padding-bottom: 0;
        }
        .timeline-item.active .timeline-item-content {
            max-height: 500px;
            padding-top: 1rem;
            padding-bottom: 1rem;
        }
        .timeline-item.active .timeline-toggle-icon {
            transform: rotate(45deg);
        }
        .timeline-toggle-icon {
            transition: transform 0.3s ease-in-out;
        }
        .chart-container {
            position: relative;
            width: 100%;
            height: 400px;
            max-height: 50vh;
        }
        @media (min-width: 768px) {
            .chart-container {
                height: 500px;
            }
        }
    </style>
</head>
<body class="antialiased">

    <header class="bg-white/80 backdrop-blur-sm sticky top-0 z-50 shadow-sm">
        <nav class="container mx-auto px-6 py-4 flex justify-between items-center">
            <div class="text-2xl font-bold text-zinc-800">
                Mohamed Othman
            </div>
            <div class="hidden md:flex space-x-8">
                <a href="#experience" class="text-zinc-600 hover:text-teal-700 transition-colors">Experience</a>
                <a href="#expertise" class="text-zinc-600 hover:text-teal-700 transition-colors">Expertise</a>
                <a href="#education" class="text-zinc-600 hover:text-teal-700 transition-colors">Education</a>
            </div>
        </nav>
    </header>

    <main class="container mx-auto px-6 py-12 md:py-20">
        
        <section id="hero" class="text-center mb-20">
            <h1 class="text-4xl md:text-6xl font-extrabold text-zinc-800 mb-4">Software QC Team Lead</h1>
            <p class="text-lg md:text-xl text-zinc-600 max-w-3xl mx-auto mb-8">
                A detail-oriented Software Testing Team Lead focused on ensuring the delivery of high-quality software. My experience covers leading QC teams, overseeing test planning and execution, driving process improvements, and collaborating across departments to meet quality objectives and deliver successful projects.
            </p>
            <a href="Mohamed-Othman-QC Team Lead-CV.pdf" download class="inline-block bg-teal-700 text-white font-bold py-3 px-8 rounded-lg hover:bg-teal-800 transition-transform transform hover:scale-105">
                Download CV
            </a>
        </section>

        <section id="experience" class="mb-20">
            <h2 class="text-3xl font-bold text-center mb-12 text-zinc-800">Career Timeline</h2>
            <div class="relative max-w-3xl mx-auto">
                <div class="absolute left-1/2 transform -translate-x-1/2 h-full w-0.5 bg-zinc-300"></div>
                <div id="timeline-container" class="space-y-12">
                </div>
            </div>
        </section>

        <section id="expertise" class="mb-20">
            <h2 class="text-3xl font-bold text-center mb-4 text-zinc-800">Core Expertise & Tools</h2>
            <p class="text-lg text-zinc-600 text-center max-w-3xl mx-auto mb-12">
                This section provides a visual overview of my primary skill areas and the technical tools I use to ensure software quality. The chart highlights my core competencies, offering a quick look at the foundations of my quality control expertise.
            </p>
            <div class="grid grid-cols-1 lg:grid-cols-5 gap-8">
                <div class="lg:col-span-3 bg-white p-6 rounded-xl shadow-md">
                    <h3 class="text-xl font-bold mb-4 text-zinc-800">Competency Overview</h3>
                    <div class="chart-container">
                        <canvas id="skillsChart"></canvas>
                    </div>
                </div>
                <div class="lg:col-span-2 bg-white p-6 rounded-xl shadow-md">
                    <h3 class="text-xl font-bold mb-4 text-zinc-800">Tools of the Trade</h3>
                    <div id="tools-container" class="grid grid-cols-2 sm:grid-cols-3 gap-4">
                    </div>
                </div>
            </div>
        </section>

        <section id="education">
            <h2 class="text-3xl font-bold text-center mb-12 text-zinc-800">Education & Certifications</h2>
            <div class="max-w-4xl mx-auto grid md:grid-cols-2 gap-8">
                <div class="bg-white p-8 rounded-xl shadow-md text-center">
                    <div class="text-5xl mb-4">🎓</div>
                    <h3 class="text-xl font-bold text-zinc-800">Bachelor of Science</h3>
                    <p class="text-zinc-600">Helwan University</p>
                    <p class="text-zinc-500 text-sm mt-1">Graduated 2016</p>
                </div>
                <div class="bg-white p-8 rounded-xl shadow-md text-center">
                    <div class="text-5xl mb-4">📜</div>
                    <h3 class="text-xl font-bold text-zinc-800">ISTQB® Certified Tester</h3>
                    <p class="text-zinc-600">Foundation Level (CTFL)</p>
                    <p class="text-zinc-500 text-sm mt-1">Issued June 2023</p>
                </div>
            </div>
        </section>

    </main>

    <footer class="bg-zinc-800 text-zinc-300 mt-20">
        <div class="container mx-auto px-6 py-8 text-center">
            <h3 class="text-2xl font-bold mb-2">Get in Touch</h3>
            <p class="mb-4">mohamedosmanmr@gmail.com | +201140530388</p>
            <p>&copy; 2025 Mohamed Othman. All rights reserved.</p>
        </div>
    </footer>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const experienceData = [
                {
                    company: "Waseet.net",
                    role: "Testing Team Lead",
                    period: "July 2023 - Present",
                    side: "left",
                    details: [
                        "Lead and mentor a team of QA engineers.",
                        "Define testing strategies, automation frameworks, and best practices.",
                        "Oversee test planning, execution, and reporting.",
                        "Collaborate with cross-functional teams to align QA processes with business goals.",
                        "Ensure timely, high-quality product releases."
                    ]
                },
                {
                    company: "Art Sketch",
                    role: "Testing Team Lead",
                    period: "Dec 2022 - Present",
                    side: "right",
                    details: [
                        "Lead a team of QC engineers and testers to ensure the delivery of high-quality software products.",
                        "Oversee test planning, execution, and reporting.",
                        "Improve testing processes and drive continuous improvement."
                    ]
                },
                {
                    company: "Waseet.net",
                    role: "Senior Software Testing",
                    period: "Sep 2022 - June 2023",
                    side: "left",
                    details: [
                        "Specialized in API Testing (Manual & Automated) to ensure seamless integration and functionality.",
                        "Executed Performance Testing and evaluated UI/UX for Web and Mobile Applications.",
                        "Developed comprehensive Test Cases and prepared detailed Bug Reports for effective issue resolution.",
                        "Applied Agile Methodology and participated in Scrum practices."
                    ]
                },
                {
                    company: "Fawry",
                    role: "Senior Software Testing",
                    period: "Aug 2021 - Sep 2022",
                    side: "right",
                    details: [
                        "Ensured seamless user experience by testing the complete API flow for the mobile application.",
                        "Conducted comprehensive testing of the dashboard, ensuring accurate data visualization and functionality.",
                        "Validated the integration of microservices APIs, verifying correct responses and interactions."
                    ]
                },
                 {
                    company: "Suiiz",
                    role: "Software Testing",
                    period: "Nov 2019 - Aug 2021",
                    side: "left",
                    details: [
                        "Developed detailed and comprehensive test cases for diverse testing scenarios.",
                        "Prepared clear and actionable bug reports to streamline issue resolution."
                    ]
                }
            ];

            const timelineContainer = document.getElementById('timeline-container');
            experienceData.forEach(item => {
                const alignClass = item.side === 'left' ? 'md:text-right' : 'md:text-left';
                const marginClass = item.side === 'left' ? 'md:mr-auto' : 'md:ml-auto';
                const detailsList = item.details.map(d => `<li class="text-zinc-600">${d}</li>`).join('');

                const timelineElement = `
                    <div class="relative">
                        <div class="md:w-1/2 ${marginClass} p-6 bg-white rounded-xl shadow-md cursor-pointer timeline-item">
                            <div class="flex justify-between items-start timeline-item-header">
                                <div>
                                    <p class="text-sm font-semibold text-teal-700">${item.period}</p>
                                    <h3 class="text-xl font-bold text-zinc-800">${item.role}</h3>
                                    <p class="text-md text-zinc-600">${item.company}</p>
                                </div>
                                <div class="timeline-toggle-icon text-teal-700 text-2xl font-thin ml-4">+</div>
                            </div>
                            <div class="timeline-item-content">
                                <ul class="list-disc list-inside mt-4 space-y-2 text-left">
                                    ${detailsList}
                                </ul>
                            </div>
                        </div>
                        <div class="absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 w-4 h-4 bg-teal-700 rounded-full border-4 border-white"></div>
                    </div>
                `;
                timelineContainer.innerHTML += timelineElement;
            });
            
            document.querySelectorAll('.timeline-item').forEach(item => {
                item.addEventListener('click', () => {
                    item.classList.toggle('active');
                });
            });

            const toolsData = ["Jira", "Postman", "Jmeter", "Apidog", "Figma"];
            const toolsContainer = document.getElementById('tools-container');
            toolsData.forEach(tool => {
                const toolElement = `
                    <div class="bg-zinc-100 p-4 rounded-lg text-center">
                        <p class="font-semibold text-zinc-700">${tool}</p>
                    </div>
                `;
                toolsContainer.innerHTML += toolElement;
            });

            const ctx = document.getElementById('skillsChart').getContext('2d');
            new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: ['API Testing (Manual/Auto)', 'Test Planning & Strategy', 'Performance Testing', 'UI/UX Testing', 'Agile & Scrum Practices', 'Mobile App Testing'],
                    datasets: [{
                        label: 'Competency Level',
                        data: [95, 90, 85, 85, 90, 80],
                        backgroundColor: 'rgba(15, 118, 110, 0.6)',
                        borderColor: 'rgba(15, 118, 110, 1)',
                        borderWidth: 1,
                        borderRadius: 4
                    }]
                },
                options: {
                    indexAxis: 'y',
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        x: {
                            beginAtZero: true,
                            max: 100,
                            grid: { display: false },
                            ticks: { display: false }
                        },
                        y: {
                           grid: { display: false },
                           ticks: {
                               font: { size: 14 }
                           }
                        }
                    },
                    plugins: {
                        legend: { display: false },
                        tooltip: {
                            enabled: true,
                            backgroundColor: '#18181b',
                            titleFont: { size: 14 },
                            bodyFont: { size: 12 },
                            callbacks: {
                                label: function(context) {
                                    return ` Expertise: ${context.raw}%`;
                                }
                            }
                        }
                    }
                }
            });

            document.querySelectorAll('a[href^="#"]').forEach(anchor => {
                anchor.addEventListener('click', function(e) {
                    e.preventDefault();
                    document.querySelector(this.getAttribute('href')).scrollIntoView({
                        behavior: 'smooth'
                    });
                });
            });
        });
    </script>
</body>
</html>
