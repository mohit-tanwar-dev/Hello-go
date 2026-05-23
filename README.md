<!DOCTYPE html>
<html lang="en" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CloudForge — Cloud Engineering Portfolio</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://unpkg.com/lucide@latest"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Oswald:wght@300;400;500&display=swap" rel="stylesheet">
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: 'Inter', sans-serif; background: #050505; color: #fff; }
        h1, h2, h3, h4 { font-family: 'Oswald', sans-serif; }

        /* Scrollbar */
        ::-webkit-scrollbar { width: 6px; }
        ::-webkit-scrollbar-track { background: #0A0A0A; }
        ::-webkit-scrollbar-thumb { background: #00ffc4; border-radius: 3px; }

        /* Animations */
        @keyframes fadeInUpBlur {
            0% { opacity: 0; transform: translateY(30px); filter: blur(8px); }
            100% { opacity: 1; transform: translateY(0); filter: blur(0); }
        }
        .animate-in { animation: fadeInUpBlur 0.8s cubic-bezier(0.2,0.8,0.2,1) both; }
        .delay-100 { animation-delay: 100ms; }
        .delay-200 { animation-delay: 200ms; }
        .delay-300 { animation-delay: 300ms; }
        .delay-400 { animation-delay: 400ms; }
        .delay-500 { animation-delay: 500ms; }
        .delay-600 { animation-delay: 600ms; }
        .delay-700 { animation-delay: 700ms; }
        .delay-800 { animation-delay: 800ms; }

        /* Scroll triggered */
        .scroll-hidden { opacity: 0; transform: translateY(30px); filter: blur(8px); transition: all 0.8s cubic-bezier(0.2,0.8,0.2,1); }
        .scroll-visible { opacity: 1; transform: translateY(0); filter: blur(0); }

        /* 3D Card */
        .card-3d { transition: transform 0.4s ease, box-shadow 0.4s ease; }
        .card-3d:hover { transform: translateY(-8px) rotateX(2deg) rotateY(2deg); box-shadow: 0 20px 60px rgba(0,255,196,0.1), 0 0 30px rgba(0,255,196,0.05); }

        /* Gradient text */
        .gradient-text { background: linear-gradient(135deg, #fff, #00ffc4); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; }

        /* Grid background */
        .grid-bg { background-image: linear-gradient(to right, rgba(255,255,255,0.03) 1px, transparent 1px), linear-gradient(to bottom, rgba(255,255,255,0.03) 1px, transparent 1px); background-size: 24px 24px; }

        /* Glow pulse */
        @keyframes glowPulse {
            0%, 100% { box-shadow: 0 0 20px rgba(0,255,196,0.2); }
            50% { box-shadow: 0 0 40px rgba(0,255,196,0.4); }
        }
        .glow-pulse { animation: glowPulse 3s ease-in-out infinite; }

        /* Float animation */
        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-12px); }
        }
        .float { animation: float 6s ease-in-out infinite; }
        .float-delay { animation: float 6s ease-in-out infinite; animation-delay: 2s; }

        /* Typing cursor */
        @keyframes blink { 0%, 50% { opacity: 1; } 51%, 100% { opacity: 0; } }
        .cursor-blink { animation: blink 1s step-end infinite; }

        /* Skill bar fill */
        .skill-fill { transition: width 1.5s cubic-bezier(0.2,0.8,0.2,1); width: 0; }
        .skill-fill.active { width: var(--fill-width); }

        /* Nav active */
        .nav-link { position: relative; }
        .nav-link::after { content: ''; position: absolute; bottom: -4px; left: 50%; transform: translateX(-50%); width: 0; height: 2px; background: #00ffc4; transition: width 0.3s ease; }
        .nav-link:hover::after, .nav-link.active::after { width: 100%; }

        /* Toast */
        @keyframes slideInRight { 0% { transform: translateX(100%); opacity: 0; } 100% { transform: translateX(0); opacity: 1; } }
        @keyframes slideOutRight { 0% { transform: translateX(0); opacity: 1; } 100% { transform: translateX(100%); opacity: 0; } }
        .toast-in { animation: slideInRight 0.4s ease both; }
        .toast-out { animation: slideOutRight 0.4s ease both; }

        /* Project card overlay */
        .project-overlay { opacity: 0; transition: opacity 0.3s ease; }
        .project-card:hover .project-overlay { opacity: 1; }
        .project-card:hover .project-img { transform: scale(1.05); }
        .project-img { transition: transform 0.5s ease; }

        /* Terminal */
        .terminal-text { font-family: 'Courier New', monospace; }

        /* Orbit animation */
        @keyframes orbit { 0% { transform: rotate(0deg) translateX(120px) rotate(0deg); } 100% { transform: rotate(360deg) translateX(120px) rotate(-360deg); } }
        .orbit-1 { animation: orbit 12s linear infinite; }
        .orbit-2 { animation: orbit 18s linear infinite reverse; }
        .orbit-3 { animation: orbit 24s linear infinite; }
    </style>
</head>
<body class="grid-bg">

    <!-- Toast Container -->
    <div id="toast-container" class="fixed top-6 right-6 z-[200] flex flex-col gap-3"></div>

    <!-- Ambient Glow -->
    <div class="fixed top-0 left-0 w-full h-full pointer-events-none z-0">
        <div class="absolute top-[-200px] left-[-200px] w-[600px] h-[600px] rounded-full bg-[#00ffc4] opacity-[0.04] blur-[120px]"></div>
        <div class="absolute bottom-[-200px] right-[-200px] w-[500px] h-[500px] rounded-full bg-[#047857] opacity-[0.06] blur-[120px]"></div>
    </div>

    <!-- Navigation -->
    <nav class="fixed top-0 left-0 right-0 z-50 backdrop-blur-md bg-[#050505]/80 border-b border-white/5">
        <div class="max-w-7xl mx-auto px-6 py-4 flex items-center justify-between">
            <a href="#hero" class="flex items-center gap-2 group">
                <div class="w-8 h-8 rounded-lg bg-gradient-to-br from-[#00ffc4] to-[#047857] flex items-center justify-center">
                    <i data-lucide="cloud" class="w-4 h-4 text-black"></i>
                </div>
                <span class="font-['Oswald'] text-xl font-300 tracking-wide">CLOUD<span class="text-[#00ffc4]">FORGE</span></span>
            </a>
            <div class="hidden md:flex items-center gap-8">
                <a href="#about" class="nav-link text-sm text-neutral-400 hover:text-white transition-colors">About</a>
                <a href="#skills" class="nav-link text-sm text-neutral-400 hover:text-white transition-colors">Skills</a>
                <a href="#projects" class="nav-link text-sm text-neutral-400 hover:text-white transition-colors">Projects</a>
                <a href="#experience" class="nav-link text-sm text-neutral-400 hover:text-white transition-colors">Experience</a>
                <a href="#contact" class="nav-link text-sm text-neutral-400 hover:text-white transition-colors">Contact</a>
            </div>
            <div class="flex items-center gap-4">
                <a href="#contact" class="hidden sm:inline-flex items-center gap-2 px-5 py-2.5 bg-[#00ffc4] text-black text-sm font-semibold rounded-lg hover:scale-105 transition-transform shadow-[0_0_20px_rgba(0,255,196,0.3)]">
                    <i data-lucide="send" class="w-4 h-4"></i>
                    Hire Me
                </a>
                <button id="mobile-toggle" class="md:hidden text-white">
                    <i data-lucide="menu" class="w-6 h-6"></i>
                </button>
            </div>
        </div>
        <!-- Mobile Menu -->
        <div id="mobile-menu" class="hidden md:hidden border-t border-white/5 bg-[#0A0A0A]/95 backdrop-blur-md">
            <div class="px-6 py-4 flex flex-col gap-4">
                <a href="#about" class="text-neutral-400 hover:text-white transition-colors mobile-link">About</a>
                <a href="#skills" class="text-neutral-400 hover:text-white transition-colors mobile-link">Skills</a>
                <a href="#projects" class="text-neutral-400 hover:text-white transition-colors mobile-link">Projects</a>
                <a href="#experience" class="text-neutral-400 hover:text-white transition-colors mobile-link">Experience</a>
                <a href="#contact" class="text-neutral-400 hover:text-white transition-colors mobile-link">Contact</a>
            </div>
        </div>
    </nav>

    <!-- Hero Section -->
    <section id="hero" class="relative min-h-screen flex items-center justify-center overflow-hidden pt-20">
        <!-- Orbital decoration -->
        <div class="absolute inset-0 flex items-center justify-center pointer-events-none">
            <div class="relative w-[300px] h-[300px] md:w-[500px] md:h-[500px]">
                <div class="orbit-1 absolute top-1/2 left-1/2 w-3 h-3 rounded-full bg-[#00ffc4] opacity-60 glow-pulse"></div>
                <div class="orbit-2 absolute top-1/2 left-1/2 w-2 h-2 rounded-full bg-[#047857] opacity-80"></div>
                <div class="orbit-3 absolute top-1/2 left-1/2 w-2 h-2 rounded-full bg-white opacity-30"></div>
                <div class="absolute inset-0 border border-white/5 rounded-full"></div>
                <div class="absolute inset-8 border border-white/[0.03] rounded-full"></div>
                <div class="absolute inset-16 border border-white/[0.02] rounded-full"></div>
            </div>
        </div>

        <div class="relative z-10 max-w-5xl mx-auto px-6 text-center">
            <!-- Status Badge -->
            <div class="animate-in inline-flex items-center gap-2 px-4 py-1.5 rounded-full border border-white/10 bg-white/[0.03] mb-8">
                <span class="w-2 h-2 rounded-full bg-[#00ffc4] animate-pulse"></span>
                <span class="text-xs text-neutral-400 uppercase tracking-wider">Available for opportunities</span>
            </div>

            <!-- Main Title -->
            <h1 class="animate-in delay-100 text-4xl sm:text-5xl md:text-7xl font-300 tracking-tight leading-[1.05] mb-6">
                Cloud Engineer<br>
                <span class="gradient-text">& Infrastructure Architect</span>
            </h1>

            <!-- Subtitle -->
            <p class="animate-in delay-200 text-base md:text-lg text-neutral-400 max-w-2xl mx-auto mb-4 leading-relaxed">
                I design, build, and automate scalable cloud infrastructure on
                <span class="text-[#00ffc4]">AWS</span>,
                <span class="text-[#00ffc4]">Azure</span>, and
                <span class="text-[#00ffc4]">GCP</span> — turning complex systems into elegant, resilient solutions.
            </p>

            <!-- Terminal Preview -->
            <div class="animate-in delay-300 inline-block mb-10 bg-[#0A0A0A] border border-white/10 rounded-lg px-5 py-3 text-sm terminal-text">
                <span class="text-[#00ffc4]">$</span> <span class="text-neutral-300" id="typing-text"></span><span class="cursor-blink text-[#00ffc4]">|</span>
            </div>

            <!-- CTA Buttons -->
            <div class="animate-in delay-400 flex flex-col sm:flex-row items-center justify-center gap-4">
                <a href="#projects" class="group inline-flex items-center gap-2 px-8 py-3.5 bg-[#00ffc4] text-black text-sm font-semibold rounded-lg hover:scale-105 transition-all shadow-[0_0_30px_rgba(0,255,196,0.3)] hover:shadow-[0_0_40px_rgba(0,255,196,0.5)]">
                    View Projects
                    <i data-lucide="arrow-right" class="w-4 h-4 group-hover:translate-x-1 transition-transform"></i>
                </a>
                <a href="#contact" class="inline-flex items-center gap-2 px-8 py-3.5 border border-white/10 text-white text-sm font-medium rounded-lg hover:bg-white/5 hover:border-[#00ffc4]/30 transition-all">
                    <i data-lucide="message-square" class="w-4 h-4"></i>
                    Get In Touch
                </a>
            </div>

            <!-- Stats -->
            <div class="animate-in delay-500 mt-16 grid grid-cols-3 gap-8 max-w-lg mx-auto">
                <div class="text-center">
                    <div class="text-2xl md:text-3xl font-['Oswald'] font-300 text-[#00ffc4]" id="stat-years">0</div>
                    <div class="text-xs text-neutral-500 uppercase tracking-wider mt-1">Years Exp</div>
                </div>
                <div class="text-center">
                    <div class="text-2xl md:text-3xl font-['Oswald'] font-300 text-[#00ffc4]" id="stat-projects">0</div>
                    <div class="text-xs text-neutral-500 uppercase tracking-wider mt-1">Projects</div>
                </div>
                <div class="text-center">
                    <div class="text-2xl md:text-3xl font-['Oswald'] font-300 text-[#00ffc4]" id="stat-certs">0</div>
                    <div class="text-xs text-neutral-500 uppercase tracking-wider mt-1">Certifications</div>
                </div>
            </div>
        </div>

        <!-- Scroll Indicator -->
        <div class="absolute bottom-8 left-1/2 -translate-x-1/2 flex flex-col items-center gap-2 animate-in delay-700">
            <span class="text-[10px] text-neutral-600 uppercase tracking-widest">Scroll</span>
            <div class="w-5 h-8 border border-white/10 rounded-full flex justify-center pt-1.5">
                <div class="w-1 h-2 bg-[#00ffc4] rounded-full animate-bounce"></div>
            </div>
        </div>
    </section>

    <!-- About Section -->
    <section id="about" class="relative py-24 md:py-32">
        <div class="max-w-7xl mx-auto px-6">
            <div class="scroll-hidden grid grid-cols-1 lg:grid-cols-12 gap-12 lg:gap-16 items-center">
                <!-- Left: Image/Visual -->
                <div class="lg:col-span-5">
                    <div class="relative">
                        <div class="aspect-[4/5] rounded-2xl overflow-hidden border border-white/10 bg-[#0A0A0A]">
                            <img src="https://picsum.photos/seed/cloudengineer/600/750.jpg" alt="Profile" class="w-full h-full object-cover opacity-80 hover:opacity-100 transition-opacity duration-500">
                        </div>
                        <!-- Floating Badge -->
                        <div class="absolute -bottom-4 -right-4 md:-right-8 bg-[#0A0A0A] border border-white/10 rounded-xl px-5 py-4 float">
                            <div class="flex items-center gap-3">
                                <div class="w-10 h-10 rounded-lg bg-[#00ffc4]/10 flex items-center justify-center">
                                    <i data-lucide="shield-check" class="w-5 h-5 text-[#00ffc4]"></i>
                                </div>
                                <div>
                                    <div class="text-xs text-neutral-500">AWS Certified</div>
                                    <div class="text-sm font-medium">Solutions Architect</div>
                                </div>
                            </div>
                        </div>
                        <!-- Floating Badge 2 -->
                        <div class="absolute -top-4 -left-4 md:-left-8 bg-[#0A0A0A] border border-white/10 rounded-xl px-5 py-4 float-delay">
                            <div class="flex items-center gap-3">
                                <div class="w-10 h-10 rounded-lg bg-[#047857]/20 flex items-center justify-center">
                                    <i data-lucide="server" class="w-5 h-5 text-[#047857]"></i>
                                </div>
                                <div>
                                    <div class="text-xs text-neutral-500">Infrastructure</div>
                                    <div class="text-sm font-medium">As Code Pro</div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Right: Content -->
                <div class="lg:col-span-7">
                    <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full border border-white/10 bg-white/[0.03] mb-6">
                        <span class="text-[10px] text-[#00ffc4] uppercase tracking-widest">About Me</span>
                    </div>
                    <h2 class="text-3xl md:text-5xl font-300 tracking-tight leading-tight mb-6">
                        Building the <span class="gradient-text">cloud backbone</span> of modern applications
                    </h2>
                    <p class="text-neutral-400 leading-relaxed mb-6">
                        I'm a Cloud Engineer with 5+ years of experience architecting and deploying production-grade infrastructure across AWS, Azure, and GCP. My passion lies in Infrastructure as Code, container orchestration, and building CI/CD pipelines that ship code reliably and fast.
                    </p>
                    <p class="text-neutral-400 leading-relaxed mb-8">
                        From designing multi-region fault-tolerant architectures to optimizing cloud spend by 40%, I bring both strategic vision and hands-on execution. I believe great infrastructure is invisible — it just works.
                    </p>

                    <!-- Info Grid -->
                    <div class="grid grid-cols-2 gap-4 mb-8">
                        <div class="flex items-center gap-3">
                            <i data-lucide="map-pin" class="w-4 h-4 text-[#00ffc4]"></i>
                            <span class="text-sm text-neutral-400">San Francisco, CA</span>
                        </div>
                        <div class="flex items-center gap-3">
                            <i data-lucide="briefcase" class="w-4 h-4 text-[#00ffc4]"></i>
                            <span class="text-sm text-neutral-400">Open to Remote</span>
                        </div>
                        <div class="flex items-center gap-3">
                            <i data-lucide="graduation-cap" class="w-4 h-4 text-[#00ffc4]"></i>
                            <span class="text-sm text-neutral-400">M.S. Computer Science</span>
                        </div>
                        <div class="flex items-center gap-3">
                            <i data-lucide="languages" class="w-4 h-4 text-[#00ffc4]"></i>
                            <span class="text-sm text-neutral-400">English, Spanish</span>
                        </div>
                    </div>

                    <a href="#contact" class="inline-flex items-center gap-2 text-[#00ffc4] text-sm font-medium hover:gap-3 transition-all group">
                        Let's work together
                        <i data-lucide="arrow-right" class="w-4 h-4 group-hover:translate-x-1 transition-transform"></i>
                    </a>
                </div>
            </div>
        </div>
    </section>

    <!-- Skills Section -->
    <section id="skills" class="relative py-24 md:py-32">
        <div class="max-w-7xl mx-auto px-6">
            <div class="scroll-hidden text-center mb-16">
                <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full border border-white/10 bg-white/[0.03] mb-6">
                    <span class="text-[10px] text-[#00ffc4] uppercase tracking-widest">Skills & Technologies</span>
                </div>
                <h2 class="text-3xl md:text-5xl font-300 tracking-tight">
                    My <span class="gradient-text">technical arsenal</span>
                </h2>
            </div>

            <!-- Skill Categories -->
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                <!-- Cloud Platforms -->
                <div class="scroll-hidden card-3d p-6 rounded-2xl bg-[#0A0A0A] border border-white/5 hover:border-[#00ffc4]/20 transition-colors group">
                    <div class="w-12 h-12 rounded-xl bg-[#00ffc4]/10 flex items-center justify-center mb-5 group-hover:scale-110 transition-transform">
                        <i data-lucide="cloud" class="w-6 h-6 text-[#00ffc4]"></i>
                    </div>
                    <h3 class="text-lg font-['Oswald'] font-300 mb-4">Cloud Platforms</h3>
                    <div class="space-y-3">
                        <div>
                            <div class="flex justify-between text-sm mb-1"><span class="text-neutral-400">AWS</span><span class="text-[#00ffc4]">95%</span></div>
                            <div class="h-1.5 bg-white/5 rounded-full overflow-hidden"><div class="skill-fill h-full bg-gradient-to-r from-[#047857] to-[#00ffc4] rounded-full" style="--fill-width: 95%"></div></div>
                        </div>
                        <div>
                            <div class="flex justify-between text-sm mb-1"><span class="text-neutral-400">Azure</span><span class="text-[#00ffc4]">85%</span></div>
                            <div class="h-1.5 bg-white/5 rounded-full overflow-hidden"><div class="skill-fill h-full bg-gradient-to-r from-[#047857] to-[#00ffc4] rounded-full" style="--fill-width: 85%"></div></div>
                        </div>
                        <div>
                            <div class="flex justify-between text-sm mb-1"><span class="text-neutral-400">Google Cloud</span><span class="text-[#00ffc4]">78%</span></div>
                            <div class="h-1.5 bg-white/5 rounded-full overflow-hidden"><div class="skill-fill h-full bg-gradient-to-r from-[#047857] to-[#00ffc4] rounded-full" style="--fill-width: 78%"></div></div>
                        </div>
                    </div>
                </div>

                <!-- IaC & DevOps -->
                <div class="scroll-hidden card-3d p-6 rounded-2xl bg-[#0A0A0A] border border-white/5 hover:border-[#00ffc4]/20 transition-colors group">
                    <div class="w-12 h-12 rounded-xl bg-[#00ffc4]/10 flex items-center justify-center mb-5 group-hover:scale-110 transition-transform">
                        <i data-lucide="file-code" class="w-6 h-6 text-[#00ffc4]"></i>
                    </div>
                    <h3 class="text-lg font-['Oswald'] font-300 mb-4">IaC & DevOps</h3>
                    <div class="space-y-3">
                        <div>
                            <div class="flex justify-between text-sm mb-1"><span class="text-neutral-400">Terraform</span><span class="text-[#00ffc4]">97%</span></div>
                            <div class="h-1.5 bg-white/5 rounded-full overflow-hidden"><div class="skill-fill h-full bg-gradient-to-r from-[#047857] to-[#00ffc4] rounded-full" style="--fill-width: 97%"></div></div>
                        </div>
                        <div>
                            <div class="flex justify-between text-sm mb-1"><span class="text-neutral-400">Kubernetes</span><span class="text-[#00ffc4]">90%</span></div>
                            <div class="h-1.5 bg-white/5 rounded-full overflow-hidden"><div class="skill-fill h-full bg-gradient-to-r from-[#047857] to-[#00ffc4] rounded-full" style="--fill-width: 90%"></div></div>
                        </div>
                        <div>
                            <div class="flex justify-between text-sm mb-1"><span class="text-neutral-400">Ansible</span><span class="text-[#00ffc4]">88%</span></div>
                            <div class="h-1.5 bg-white/5 rounded-full overflow-hidden"><div class="skill-fill h-full bg-gradient-to-r from-[#047857] to-[#00ffc4] rounded-full" style="--fill-width: 88%"></div></div>
                        </div>
                    </div>
                </div>

                <!-- CI/CD & Automation -->
                <div class="scroll-hidden card-3d p-6 rounded-2xl bg-[#0A0A0A] border border-white/5 hover:border-[#00ffc4]/20 transition-colors group">
                    <div class="w-12 h-12 rounded-xl bg-[#00ffc4]/10 flex items-center justify-center mb-5 group-hover:scale-110 transition-transform">
                        <i data-lucide="git-branch" class="w-6 h-6 text-[#00ffc4]"></i>
                    </div>
                    <h3 class="text-lg font-['Oswald'] font-300 mb-4">CI/CD & Automation</h3>
                    <div class="space-y-3">
                        <div>
                            <div class="flex justify-between text-sm mb-1"><span class="text-neutral-400">GitHub Actions</span><span class="text-[#00ffc4]">92%</span></div>
                            <div class="h-1.5 bg-white/5 rounded-full overflow-hidden"><div class="skill-fill h-full bg-gradient-to-r from-[#047857] to-[#00ffc4] rounded-full" style="--fill-width: 92%"></div></div>
                        </div>
                        <div>
                            <div class="flex justify-between text-sm mb-1"><span class="text-neutral-400">Jenkins</span><span class="text-[#00ffc4]">85%</span></div>
                            <div class="h-1.5 bg-white/5 rounded-full overflow-hidden"><div class="skill-fill h-full bg-gradient-to-r from-[#047857] to-[#00ffc4] rounded-full" style="--fill-width: 85%"></div></div>
                        </div>
                        <div>
                            <div class="flex justify-between text-sm mb-1"><span class="text-neutral-400">ArgoCD</span><span class="text-[#00ffc4]">80%</span></div>
                            <div class="h-1.5 bg-white/5 rounded-full overflow-hidden"><div class="skill-fill h-full bg-gradient-to-r from-[#047857] to-[#00ffc4] rounded-full" style="--fill-width: 80%"></div></div>
                        </div>
                    </div>
                </div>

                <!-- Containers -->
                <div class="scroll-hidden card-3d p-6 rounded-2xl bg-[#0A0A0A] border border-white/5 hover:border-[#00ffc4]/20 transition-colors group">
                    <div class="w-12 h-12 rounded-xl bg-[#00ffc4]/10 flex items-center justify-center mb-5 group-hover:scale-110 transition-transform">
                        <i data-lucide="box" class="w-6 h-6 text-[#00ffc4]"></i>
                    </div>
                    <h3 class="text-lg font-['Oswald'] font-300 mb-4">Containers & Orchestration</h3>
                    <div class="flex flex-wrap gap-2 mt-3">
                        <span class="px-3 py-1 text-xs rounded-full border border-white/10 bg-white/[0.03] text-neutral-300">Docker</span>
                        <span class="px-3 py-1 text-xs rounded-full border border-white/10 bg-white/[0.03] text-neutral-300">EKS</span>
                        <span class="px-3 py-1 text-xs rounded-full border border-white/10 bg-white/[0.03] text-neutral-300">AKS</span>
                        <span class="px-3 py-1 text-xs rounded-full border border-white/10 bg-white/[0.03] text-neutral-300">GKE</span>
                        <span class="px-3 py-1 text-xs rounded-full border border-white/10 bg-white/[0.03] text-neutral-300">Helm</span>
                        <span class="px-3 py-1 text-xs rounded-full border border-white/10 bg-white/[0.03] text-neutral-300">Istio</span>
                        <span class="px-3 py-1 text-xs rounded-full border border-[#00ffc4]/20 bg-[#00ffc4]/5 text-[#00ffc4]">K8s</span>
                    </div>
                </div>

                <!-- Monitoring -->
                <div class="scroll-hidden card-3d p-6 rounded-2xl bg-[#0A0A0A] border border-white/5 hover:border-[#00ffc4]/20 transition-colors group">
                    <div class="w-12 h-12 rounded-xl bg-[#00ffc4]/10 flex items-center justify-center mb-5 group-hover:scale-110 transition-transform">
                        <i data-lucide="activity" class="w-6 h-6 text-[#00ffc4]"></i>
                    </div>
                    <h3 class="text-lg font-['Oswald'] font-300 mb-4">Monitoring & Observability</h3>
                    <div class="flex flex-wrap gap-2 mt-3">
                        <span class="px-3 py-1 text-xs rounded-full border border-white/10 bg-white/[0.03] text-neutral-300">Prometheus</span>
                        <span class="px-3 py-1 text-xs rounded-full border border-white/10 bg-white/[0.03] text-neutral-300">Grafana</span>
                        <span class="px-3 py-1 text-xs rounded-full border border-white/10 bg-white/[0.03] text-neutral-300">Datadog</span>
                        <span class="px-3 py-1 text-xs rounded-full border border-white/10 bg-white/[0.03] text-neutral-300">ELK Stack</span>
                        <span class="px-3 py-1 text-xs rounded-full border border-white/10 bg-white/[0.03] text-neutral-300">CloudWatch</span>
                        <span class="px-3 py-1 text-xs rounded-full border border-[#00ffc4]/20 bg-[#00ffc4]/5 text-[#00ffc4]">OpenTelemetry</span>
                    </div>
                </div>

                <!-- Scripting -->
                <div class="scroll-hidden card-3d p-6 rounded-2xl bg-[#0A0A0A] border border-white/5 hover:border-[#00ffc4]/20 transition-colors group">
                    <div class="w-12 h-12 rounded-xl bg-[#00ffc4]/10 flex items-center justify-center mb-5 group-hover:scale-110 transition-transform">
                        <i data-lucide="terminal" class="w-6 h-6 text-[#00ffc4]"></i>
                    </div>
                    <h3 class="text-lg font-['Oswald'] font-300 mb-4">Scripting & Languages</h3>
                    <div class="flex flex-wrap gap-2 mt-3">
                        <span class="px-3 py-1 text-xs rounded-full border border-white/10 bg-white/[0.03] text-neutral-300">Python</span>
                        <span class="px-3 py-1 text-xs rounded-full border border-white/10 bg-white/[0.03] text-neutral-300">Bash</span>
                        <span class="px-3 py-1 text-xs rounded-full border border-white/10 bg-white/[0.03] text-neutral-300">Go</span>
                        <span class="px-3 py-1 text-xs rounded-full border border-white/10 bg-white/[0.03] text-neutral-300">Node.js</span>
                        <span class="px-3 py-1 text-xs rounded-full border border-[#00ffc4]/20 bg-[#00ffc4]/5 text-[#00ffc4]">HCL</span>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Projects Section -->
    <section id="projects" class="relative py-24 md:py-32">
        <div class="max-w-7xl mx-auto px-6">
            <div class="scroll-hidden text-center mb-16">
                <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full border border-white/10 bg-white/[0.03] mb-6">
                    <span class="text-[10px] text-[#00ffc4] uppercase tracking-widest">Featured Work</span>
                </div>
                <h2 class="text-3xl md:text-5xl font-300 tracking-tight">
                    Infrastructure <span class="gradient-text">that scales</span>
                </h2>
            </div>

            <!-- Project Filter -->
            <div class="scroll-hidden flex items-center justify-center gap-2 mb-12 flex-wrap">
                <button class="filter-btn active px-4 py-2 text-sm rounded-lg border border-white/10 bg-white/[0.03] text-neutral-400 hover:text-white hover:border-[#00ffc4]/30 transition-all" data-filter="all">All</button>
                <button class="filter-btn px-4 py-2 text-sm rounded-lg border border-white/10 bg-white/[0.03] text-neutral-400 hover:text-white hover:border-[#00ffc4]/30 transition-all" data-filter="aws">AWS</button>
                <button class="filter-btn px-4 py-2 text-sm rounded-lg border border-white/10 bg-white/[0.03] text-neutral-400 hover:text-white hover:border-[#00ffc4]/30 transition-all" data-filter="k8s">Kubernetes</button>
                <button class="filter-btn px-4 py-2 text-sm rounded-lg border border-white/10 bg-white/[0.03] text-neutral-400 hover:text-white hover:border-[#00ffc4]/30 transition-all" data-filter="iac">IaC</button>
                <button class="filter-btn px-4 py-2 text-sm rounded-lg border border-white/10 bg-white/[0.03] text-neutral-400 hover:text-white hover:border-[#00ffc4]/30 transition-all" data-filter="devops">DevOps</button>
            </div>

            <!-- Projects Grid -->
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6" id="projects-grid">
                <!-- Project 1 -->
                <div class="scroll-hidden project-card card-3d rounded-2xl bg-[#0A0A0A] border border-white/5 hover:border-[#00ffc4]/20 overflow-hidden transition-all group" data-category="aws iac">
                    <div class="relative aspect-video overflow-hidden">
                        <img src="https://picsum.photos/seed/multicloudarch/600/340.jpg" alt="Multi-Region Architecture" class="project-img w-full h-full object-cover opacity-70">
                        <div class="project-overlay absolute inset-0 bg-gradient-to-t from-[#0A0A0A] via-transparent to-transparent flex items-end p-4">
                            <div class="flex gap-2">
                                <a href="#" class="px-3 py-1.5 text-xs bg-[#00ffc4] text-black rounded-lg font-semibold hover:scale-105 transition-transform flex items-center gap-1">
                                    <i data-lucide="external-link" class="w-3 h-3"></i> Live
                                </a>
                                <a href="#" class="px-3 py-1.5 text-xs border border-white/20 text-white rounded-lg font-medium hover:bg-white/10 transition-colors flex items-center gap-1">
                                    <i data-lucide="github" class="w-3 h-3"></i> Code
                                </a>
                            </div>
                        </div>
                    </div>
                    <div class="p-6">
                        <div class="flex items-center gap-2 mb-3">
                            <span class="px-2 py-0.5 text-[10px] uppercase tracking-wider rounded-full border border-[#00ffc4]/20 bg-[#00ffc4]/5 text-[#00ffc4]">AWS</span>
                            <span class="px-2 py-0.5 text-[10px] uppercase tracking-wider rounded-full border border-white/10 bg-white/[0.03] text-neutral-400">Terraform</span>
                        </div>
                        <h3 class="text-lg font-['Oswald'] font-300 mb-2">Multi-Region HA Architecture</h3>
                        <p class="text-sm text-neutral-400 leading-relaxed">Designed a multi-region, active-active architecture on AWS with automated failover, achieving 99.99% uptime SLA across 3 regions.</p>
                    </div>
                </div>

                <!-- Project 2 -->
                <div class="scroll-hidden project-card card-3d rounded-2xl bg-[#0A0A0A] border border-white/5 hover:border-[#00ffc4]/20 overflow-hidden transition-all group" data-category="k8s devops">
                    <div class="relative aspect-video overflow-hidden">
                        <img src="https://picsum.photos/seed/k8scluster/600/340.jpg" alt="K8s Cluster" class="project-img w-full h-full object-cover opacity-70">
                        <div class="project-overlay absolute inset-0 bg-gradient-to-t from-[#0A0A0A] via-transparent to-transparent flex items-end p-4">
                            <div class="flex gap-2">
                                <a href="#" class="px-3 py-1.5 text-xs border border-white/20 text-white rounded-lg font-medium hover:bg-white/10 transition-colors flex items-center gap-1">
                                    <i data-lucide="github" class="w-3 h-3"></i> Code
                                </a>
                            </div>
                        </div>
                    </div>
                    <div class="p-6">
                        <div class="flex items-center gap-2 mb-3">
                            <span class="px-2 py-0.5 text-[10px] uppercase tracking-wider rounded-full border border-[#00ffc4]/20 bg-[#00ffc4]/5 text-[#00ffc4]">K8s</span>
                            <span class="px-2 py-0.5 text-[10px] uppercase tracking-wider rounded-full border border-white/10 bg-white/[0.03] text-neutral-400">Helm</span>
                        </div>
                        <h3 class="text-lg font-['Oswald'] font-300 mb-2">EKS Cluster Orchestration</h3>
                        <p class="text-sm text-neutral-400 leading-relaxed">Built and managed production EKS clusters handling 50K+ req/s with Istio service mesh, auto-scaling, and zero-downtime deployments.</p>
                    </div>
                </div>

                <!-- Project 3 -->
                <div class="scroll-hidden project-card card-3d rounded-2xl bg-[#0A0A0A] border border-white/5 hover:border-[#00ffc4]/20 overflow-hidden transition-all group" data-category="iac devops">
                    <div class="relative aspect-video overflow-hidden">
                        <img src="https://picsum.photos/seed/cicdpipeline/600/340.jpg" alt="CI/CD Pipeline" class="project-img w-full h-full object-cover opacity-70">
                        <div class="project-overlay absolute inset-0 bg-gradient-to-t from-[#0A0A0A] via-transparent to-transparent flex items-end p-4">
                            <div class="flex gap-2">
                                <a href="#" class="px-3 py-1.5 text-xs bg-[#00ffc4] text-black rounded-lg font-semibold hover:scale-105 transition-transform flex items-center gap-1">
                                    <i data-lucide="external-link" class="w-3 h-3"></i> Live
                                </a>
                                <a href="#" class="px-3 py-1.5 text-xs border border-white/20 text-white rounded-lg font-medium hover:bg-white/10 transition-colors flex items-center gap-1">
                                    <i data-lucide="github" class="w-3 h-3"></i> Code
                                </a>
                            </div>
                        </div>
                    </div>
                    <div class="p-6">
                        <div class="flex items-center gap-2 mb-3">
                            <span class="px-2 py-0.5 text-[10px] uppercase tracking-wider rounded-full border border-[#00ffc4]/20 bg-[#00ffc4]/5 text-[#00ffc4]">DevOps</span>
                            <span class="px-2 py-0.5 text-[10px] uppercase tracking-wider rounded-full border border-white/10 bg-white/[0.03] text-neutral-400">GitHub Actions</span>
                        </div>
                        <h3 class="text-lg font-['Oswald'] font-300 mb-2">GitOps CI/CD Pipeline</h3>
                        <p class="text-sm text-neutral-400 leading-relaxed">Implemented a full GitOps workflow with ArgoCD, reducing deployment time from 45 minutes to under 3 minutes with automated rollbacks.</p>
                    </div>
                </div>

                <!-- Project 4 -->
                <div class="scroll-hidden project-card card-3d rounded-2xl bg-[#0A0A0A] border border-white/5 hover:border-[#00ffc4]/20 overflow-hidden transition-all group" data-category="aws devops">
                    <div class="relative aspect-video overflow-hidden">
                        <img src="https://picsum.photos/seed/serverlessarch/600/340.jpg" alt="Serverless" class="project-img w-full h-full object-cover opacity-70">
                        <div class="project-overlay absolute inset-0 bg-gradient-to-t from-[#0A0A0A] via-transparent to-transparent flex items-end p-4">
                            <div class="flex gap-2">
                                <a href="#" class="px-3 py-1.5 text-xs border border-white/20 text-white rounded-lg font-medium hover:bg-white/10 transition-colors flex items-center gap-1">
                                    <i data-lucide="github" class="w-3 h-3"></i> Code
                                </a>
                            </div>
                        </div>
                    </div>
                    <div class="p-6">
                        <div class="flex items-center gap-2 mb-3">
                            <span class="px-2 py-0.5 text-[10px] uppercase tracking-wider rounded-full border border-[#00ffc4]/20 bg-[#00ffc4]/5 text-[#00ffc4]">AWS</span>
                            <span class="px-2 py-0.5 text-[10px] uppercase tracking-wider rounded-full border border-white/10 bg-white/[0.03] text-neutral-400">Lambda</span>
                        </div>
                        <h3 class="text-lg font-['Oswald'] font-300 mb-2">Serverless Data Pipeline</h3>
                        <p class="text-sm text-neutral-400 leading-relaxed">Built an event-driven serverless pipeline processing 2M+ events/day using Lambda, Step Functions, and DynamoDB with zero server management.</p>
                    </div>
                </div>

                <!-- Project 5 -->
                <div class="scroll-hidden project-card card-3d rounded-2xl bg-[#0A0A0A] border border-white/5 hover:border-[#00ffc4]/20 overflow-hidden transition-all group" data-category="k8s iac">
                    <div class="relative aspect-video overflow-hidden">
                        <img src="https://picsum.photos/seed/monitoringdash/600/340.jpg" alt="Monitoring" class="project-img w-full h-full object-cover opacity-70">
                        <div class="project-overlay absolute inset-0 bg-gradient-to-t from-[#0A0A0A] via-transparent to-transparent flex items-end p-4">
                            <div class="flex gap-2">
                                <a href="#" class="px-3 py-1.5 text-xs bg-[#00ffc4] text-black rounded-lg font-semibold hover:scale-105 transition-transform flex items-center gap-1">
                                    <i data-lucide="external-link" class="w-3 h-3"></i> Live
                                </a>
                                <a href="#" class="px-3 py-1.5 text-xs border border-white/20 text-white rounded-lg font-medium hover:bg-white/10 transition-colors flex items-center gap-1">
                                    <i data-lucide="github" class="w-3 h-3"></i> Code
                                </a>
                            </div>
                        </div>
                    </div>
                    <div class="p-6">
                        <div class="flex items-center gap-2 mb-3">
                            <span class="px-2 py-0.5 text-[10px] uppercase tracking-wider rounded-full border border-[#00ffc4]/20 bg-[#00ffc4]/5 text-[#00ffc4]">K8s</span>
                            <span class="px-2 py-0.5 text-[10px] uppercase tracking-wider rounded-full border border-white/10 bg-white/[0.03] text-neutral-400">Prometheus</span>
                        </div>
                        <h3 class="text-lg font-['Oswald'] font-300 mb-2">Full-Stack Observability</h3>
                        <p class="text-sm text-neutral-400 leading-relaxed">Deployed comprehensive monitoring with Prometheus, Grafana, and OpenTelemetry across 200+ microservices with custom SLI/SLO dashboards.</p>
                    </div>
                </div>

                <!-- Project 6 -->
                <div class="scroll-hidden project-card card-3d rounded-2xl bg-[#0A0A0A] border border-white/5 hover:border-[#00ffc4]/20 overflow-hidden transition-all group" data-category="iac aws">
                    <div class="relative aspect-video overflow-hidden">
                        <img src="https://picsum.photos/seed/terraformmod/600/340.jpg" alt="Terraform" class="project-img w-full h-full object-cover opacity-70">
                        <div class="project-overlay absolute inset-0 bg-gradient-to-t from-[#0A0A0A] via-transparent to-transparent flex items-end p-4">
                            <div class="flex gap-2">
                                <a href="#" class="px-3 py-1.5 text-xs border border-white/20 text-white rounded-lg font-medium hover:bg-white/10 transition-colors flex items-center gap-1">
                                    <i data-lucide="github" class="w-3 h-3"></i> Code
                                </a>
                            </div>
                        </div>
                    </div>
                    <div class="p-6">
                        <div class="flex items-center gap-2 mb-3">
                            <span class="px-2 py-0.5 text-[10px] uppercase tracking-wider rounded-full border border-[#00ffc4]/20 bg-[#00ffc4]/5 text-[#00ffc4]">IaC</span>
                            <span class="px-2 py-0.5 text-[10px] uppercase tracking-wider rounded-full border border-white/10 bg-white/[0.03] text-neutral-400">Terraform</span>
                        </div>
                        <h3 class="text-lg font-['Oswald'] font-300 mb-2">Terraform Module Library</h3>
                        <p class="text-sm text-neutral-400 leading-relaxed">Created an open-source Terraform module library with 30+ reusable modules, adopted by 15+ teams and achieving 2K+ GitHub stars.</p>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Experience & Certifications -->
    <section id="experience" class="relative py-24 md:py-32">
        <div class="max-w-7xl mx-auto px-6">
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-16">
                <!-- Experience -->
                <div class="scroll-hidden">
                    <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full border border-white/10 bg-white/[0.03] mb-6">
                        <span class="text-[10px] text-[#00ffc4] uppercase tracking-widest">Experience</span>
                    </div>
                    <h2 class="text-3xl md:text-4xl font-300 tracking-tight mb-10">
                        Professional <span class="gradient-text">journey</span>
                    </h2>

                    <div class="relative pl-8 border-l border-white/10 space-y-10">
                        <!-- Job 1 -->
                        <div class="relative group">
                            <div class="absolute -left-[41px] top-1 w-4 h-4 rounded-full border-2 border-[#00ffc4] bg-[#050505] group-hover:bg-[#00ffc4] transition-colors"></div>
                            <div class="p-5 rounded-xl bg-[#0A0A0A] border border-white/5 hover:border-[#00ffc4]/20 transition-colors">
                                <div class="flex items-start justify-between mb-2">
                                    <div>
                                        <h3 class="text-base font-medium">Senior Cloud Engineer</h3>
                                        <p class="text-sm text-[#00ffc4]">TechCorp Inc.</p>
                                    </div>
                                    <span class="text-xs text-neutral-500 shrink-0">2022 — Present</span>
                                </div>
                                <p class="text-sm text-neutral-400 leading-relaxed">Lead cloud infrastructure team. Architected multi-region AWS setup serving 10M+ users. Reduced infrastructure costs by 40% through optimization.</p>
                            </div>
                        </div>
                        <!-- Job 2 -->
                        <div class="relative group">
                            <div class="absolute -left-[41px] top-1 w-4 h-4 rounded-full border-2 border-white/20 bg-[#050505] group-hover:border-[#00ffc4] group-hover:bg-[#00ffc4] transition-colors"></div>
                            <div class="p-5 rounded-xl bg-[#0A0A0A] border border-white/5 hover:border-[#00ffc4]/20 transition-colors">
                                <div class="flex items-start justify-between mb-2">
                                    <div>
                                        <h3 class="text-base font-medium">Cloud Infrastructure Engineer</h3>
                                        <p class="text-sm text-[#047857]">DataFlow Systems</p>
                                    </div>
                                    <span class="text-xs text-neutral-500 shrink-0">2020 — 2022</span>
                                </div>
                                <p class="text-sm text-neutral-400 leading-relaxed">Built Kubernetes clusters from scratch. Implemented GitOps workflows and CI/CD pipelines serving 50+ microservices deployments daily.</p>
                            </div>
                        </div>
                        <!-- Job 3 -->
                        <div class="relative group">
                            <div class="absolute -left-[41px] top-1 w-4 h-4 rounded-full border-2 border-white/20 bg-[#050505] group-hover:border-[#00ffc4] group-hover:bg-[#00ffc4] transition-colors"></div>
                            <div class="p-5 rounded-xl bg-[#0A0A0A] border border-white/5 hover:border-[#00ffc4]/20 transition-colors">
                                <div class="flex items-start justify-between mb-2">
                                    <div>
                                        <h3 class="text-base font-medium">DevOps Engineer</h3>
                                        <p class="text-sm text-neutral-500">CloudStart Labs</p>
                                    </div>
                                    <span class="text-xs text-neutral-500 shrink-0">2019 — 2020</span>
                                </div>
                                <p class="text-sm text-neutral-400 leading-relaxed">Migrated legacy on-prem infrastructure to AWS. Set up Terraform modules, monitoring, and automated backup solutions for disaster recovery.</p>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Certifications -->
                <div class="scroll-hidden">
                    <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full border border-white/10 bg-white/[0.03] mb-6">
                        <span class="text-[10px] text-[#00ffc4] uppercase tracking-widest">Certifications</span>
                    </div>
                    <h2 class="text-3xl md:text-4xl font-300 tracking-tight mb-10">
                        Verified <span class="gradient-text">expertise</span>
                    </h2>

                    <div class="space-y-4">
                        <!-- Cert 1 -->
                        <div class="card-3d p-5 rounded-xl bg-[#0A0A0A] border border-white/5 hover:border-[#00ffc4]/20 transition-colors group flex items-center gap-5">
                            <div class="w-16 h-16 shrink-0 rounded-xl overflow-hidden bg-[#FF9900]/10 flex items-center justify-center">
                                <svg class="w-10 h-10" viewBox="0 0 24 24" fill="#FF9900"><path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5"/></svg>
                            </div>
                            <div class="flex-1">
                                <h3 class="text-base font-medium group-hover:text-[#00ffc4] transition-colors">AWS Solutions Architect — Professional</h3>
                                <p class="text-xs text-neutral-500 mt-1">Amazon Web Services • Validated 2023</p>
                            </div>
                            <i data-lucide="badge-check" class="w-5 h-5 text-[#00ffc4] shrink-0"></i>
                        </div>
                        <!-- Cert 2 -->
                        <div class="card-3d p-5 rounded-xl bg-[#0A0A0A] border border-white/5 hover:border-[#00ffc4]/20 transition-colors group flex items-center gap-5">
                            <div class="w-16 h-16 shrink-0 rounded-xl overflow-hidden bg-[#0078D4]/10 flex items-center justify-center">
                                <svg class="w-10 h-10" viewBox="0 0 24 24" fill="#0078D4"><path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm-1 15h-2v-6h2v6zm4 0h-2v-6h2v6zm-2-8c-.55 0-1-.45-1-1s.45-1 1-1 1 .45 1 1-.45 1-1 1z"/></svg>
                            </div>
                            <div class="flex-1">
                                <h3 class="text-base font-medium group-hover:text-[#00ffc4] transition-colors">Azure Administrator Associate</h3>
                                <p class="text-xs text-neutral-500 mt-1">Microsoft Azure • Validated 2023</p>
                            </div>
                            <i data-lucide="badge-check" class="w-5 h-5 text-[#00ffc4] shrink-0"></i>
                        </div>
                        <!-- Cert 3 -->
                        <div class="card-3d p-5 rounded-xl bg-[#0A0A0A] border border-white/5 hover:border-[#00ffc4]/20 transition-colors group flex items-center gap-5">
                            <div class="w-16 h-16 shrink-0 rounded-xl overflow-hidden bg-[#326CE5]/10 flex items-center justify-center">
                                <svg class="w-10 h-10" viewBox="0 0 24 24" fill="#326CE5"><path d="M12 2L3.5 7v10L12 22l8.5-5V7L12 2zm0 2.5l6 3.5v7l-6 3.5-6-3.5V8l6-3.5z"/></svg>
                            </div>
                            <div class="flex-1">
                                <h3 class="text-base font-medium group-hover:text-[#00ffc4] transition-colors">Certified Kubernetes Administrator (CKA)</h3>
                                <p class="text-xs text-neutral-500 mt-1">CNCF • Validated 2022</p>
                            </div>
                            <i data-lucide="badge-check" class="w-5 h-5 text-[#00ffc4] shrink-0"></i>
                        </div>
                        <!-- Cert 4 -->
                        <div class="card-3d p-5 rounded-xl bg-[#0A0A0A] border border-white/5 hover:border-[#00ffc4]/20 transition-colors group flex items-center gap-5">
                            <div class="w-16 h-16 shrink-0 rounded-xl overflow-hidden bg-[#7B42BC]/10 flex items-center justify-center">
                                <svg class="w-10 h-10" viewBox="0 0 24 24" fill="#7B42BC"><path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm-2 15l-5-5 1.41-1.41L10 14.17l7.59-7.59L19 8l-9 9z"/></svg>
                            </div>
                            <div class="flex-1">
                                <h3 class="text-base font-medium group-hover:text-[#00ffc4] transition-colors">HashiCorp Terraform Associate</h3>
                                <p class="text-xs text-neutral-500 mt-1">HashiCorp • Validated 2022</p>
                            </div>
                            <i data-lucide="badge-check" class="w-5 h-5 text-[#00ffc4] shrink-0"></i>
                        </div>
                        <!-- Cert 5 -->
                        <div class="card-3d p-5 rounded-xl bg-[#0A0A0A] border border-white/5 hover:border-[#00ffc4]/20 transition-colors group flex items-center gap-5">
                            <div class="w-16 h-16 shrink-0 rounded-xl overflow-hidden bg-[#E535AB]/10 flex items-center justify-center">
                                <svg class="w-10 h-10" viewBox="0 0 24 24" fill="#E535AB"><circle cx="12" cy="12" r="10"/></svg>
                            </div>
                            <div class="flex-1">
                                <h3 class="text-base font-medium group-hover:text-[#00ffc4] transition-colors">GCP Professional Cloud Architect</h3>
                                <p class="text-xs text-neutral-500 mt-1">Google Cloud • Validated 2023</p>
                            </div>
                            <i data-lucide="badge-check" class="w-5 h-5 text-[#00ffc4] shrink-0"></i>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Terminal / Code Showcase -->
    <section class="relative py-24 md:py-32">
        <div class="max-w-5xl mx-auto px-6">
            <div class="scroll-hidden">
                <div class="rounded-2xl bg-[#0A0A0A] border border-white/10 overflow-hidden shadow-[0_0_30px_rgba(0,255,196,0.05)]">
                    <!-- Terminal Header -->
                    <div class="flex items-center gap-2 px-5 py-3 border-b border-white/5">
                        <div class="w-3 h-3 rounded-full bg-red-500/80"></div>
                        <div class="w-3 h-3 rounded-full bg-yellow-500/80"></div>
                        <div class="w-3 h-3 rounded-full bg-green-500/80"></div>
                        <span class="text-xs text-neutral-500 ml-3 terminal-text">main.tf — Terraform Configuration</span>
                    </div>
                    <!-- Terminal Body -->
                    <div class="p-6 terminal-text text-sm leading-relaxed overflow-x-auto">
                        <div><span class="text-[#00ffc4]">resource</span> <span class="text-yellow-300">"aws_ecs_cluster"</span> <span class="text-green-300">"production"</span> {</div>
                        <div class="pl-4"><span class="text-neutral-500">name</span> = <span class="text-orange-300">"prod-cluster-${var.environment}"</span></div>
                        <div class="pl-4"><span class="text-neutral-500">setting</span> {</div>
                        <div class="pl-8"><span class="text-neutral-500">name</span>  = <span class="text-orange-300">"containerInsights"</span></div>
                        <div class="pl-8"><span class="text-neutral-500">value</span> = <span class="text-orange-300">"enabled"</span></div>
                        <div class="pl-4">}</div>
                        <div>}</div>
                        <br>
                        <div><span class="text-[#00ffc4]">module</span> <span class="text-green-300">"vpc"</span> {</div>
                        <div class="pl-4"><span class="text-neutral-500">source</span>  = <span class="text-orange-300">"./modules/vpc"</span></div>
                        <div class="pl-4"><span class="text-neutral-500">cidr</span>    = <span class="text-orange-300">"10.0.0.0/16"</span></div>
                        <div class="pl-4"><span class="text-neutral-500">azs</span>     = <span class="text-orange-300">["us-east-1a", "us-east-1b", "us-east-1c"]</span></div>
                        <div>}</div>
                        <br>
                        <div><span class="text-[#00ffc4]">output</span> <span class="text-green-300">"cluster_arn"</span> {</div>
                        <div class="pl-4"><span class="text-neutral-500">value</span> = <span class="text-blue-300">aws_ecs_cluster.production.arn</span></div>
                        <div>}</div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="relative py-24 md:py-32">
        <div class="max-w-5xl mx-auto px-6">
            <div class="scroll-hidden text-center mb-12">
                <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full border border-white/10 bg-white/[0.03] mb-6">
                    <span class="text-[10px] text-[#00ffc4] uppercase tracking-widest">Get In Touch</span>
                </div>
                <h2 class="text-3xl md:text-5xl font-300 tracking-tight mb-4">
                    Let's build <span class="gradient-text">something great</span>
                </h2>
                <p class="text-neutral-400 max-w-lg mx-auto">Have a cloud project in mind? Looking for infrastructure expertise? I'd love to hear from you.</p>
            </div>

            <div class="scroll-hidden grid grid-cols-1 lg:grid-cols-5 gap-8">
                <!-- Contact Info -->
                <div class="lg:col-span-2 space-y-4">
                    <a href="mailto:hello@cloudforge.dev" class="flex items-center gap-4 p-4 rounded-xl bg-[#0A0A0A] border border-white/5 hover:border-[#00ffc4]/20 transition-colors group">
                        <div class="w-10 h-10 rounded-lg bg-[#00ffc4]/10 flex items-center justify-center group-hover:scale-110 transition-transform">
                            <i data-lucide="mail" class="w-5 h-5 text-[#00ffc4]"></i>
                        </div>
                        <div>
                            <div class="text-xs text-neutral-500">Email</div>
                            <div class="text-sm">hello@cloudforge.dev</div>
                        </div>
                    </a>
                    <a href="#" class="flex items-center gap-4 p-4 rounded-xl bg-[#0A0A0A] border border-white/5 hover:border-[#00ffc4]/20 transition-colors group">
                        <div class="w-10 h-10 rounded-lg bg-[#00ffc4]/10 flex items-center justify-center group-hover:scale-110 transition-transform">
                            <i data-lucide="linkedin" class="w-5 h-5 text-[#00ffc4]"></i>
                        </div>
                        <div>
                            <div class="text-xs text-neutral-500">LinkedIn</div>
                            <div class="text-sm">linkedin.com/in/cloudforge</div>
                        </div>
                    </a>
                    <a href="#" class="flex items-center gap-4 p-4 rounded-xl bg-[#0A0A0A] border border-white/5 hover:border-[#00ffc4]/20 transition-colors group">
                        <div class="w-10 h-10 rounded-lg bg-[#00ffc4]/10 flex items-center justify-center group-hover:scale-110 transition-transform">
                            <i data-lucide="github" class="w-5 h-5 text-[#00ffc4]"></i>
                        </div>
                        <div>
                            <div class="text-xs text-neutral-500">GitHub</div>
                            <div class="text-sm">github.com/cloudforge</div>
                        </div>
                    </a>
                    <a href="#" class="flex items-center gap-4 p-4 rounded-xl bg-[#0A0A0A] border border-white/5 hover:border-[#00ffc4]/20 transition-colors group">
                        <div class="w-10 h-10 rounded-lg bg-[#00ffc4]/10 flex items-center justify-center group-hover:scale-110 transition-transform">
                            <i data-lucide="file-text" class="w-5 h-5 text-[#00ffc4]"></i>
                        </div>
                        <div>
                            <div class="text-xs text-neutral-500">Resume</div>
                            <div class="text-sm">Download PDF</div>
                        </div>
                    </a>
                </div>

                <!-- Contact Form -->
                <div class="lg:col-span-3">
                    <form id="contact-form" class="p-6 md:p-8 rounded-2xl bg-[#0A0A0A] border border-white/5 space-y-5">
                        <div class="grid grid-cols-1 sm:grid-cols-2 gap-5">
                            <div>
                                <label class="text-xs text-neutral-500 uppercase tracking-wider block mb-2">Name</label>
                                <input type="text" id="form-name" required placeholder="John Doe" class="w-full px-4 py-3 rounded-lg bg-white/[0.03] border border-white/10 text-sm text-white placeholder-neutral-600 focus:outline-none focus:border-[#00ffc4]/50 focus:ring-1 focus:ring-[#00ffc4]/20 transition-colors">
                            </div>
                            <div>
                                <label class="text-xs text-neutral-500 uppercase tracking-wider block mb-2">Email</label>
                                <input type="email" id="form-email" required placeholder="john@example.com" class="w-full px-4 py-3 rounded-lg bg-white/[0.03] border border-white/10 text-sm text-white placeholder-neutral-600 focus:outline-none focus:border-[#00ffc4]/50 focus:ring-1 focus:ring-[#00ffc4]/20 transition-colors">
                            </div>
                        </div>
                        <div>
                            <label class="text-xs text-neutral-500 uppercase tracking-wider block mb-2">Subject</label>
                            <select id="form-subject" class="w-full px-4 py-3 rounded-lg bg-white/[0.03] border border-white/10 text-sm text-neutral-400 focus:outline-none focus:border-[#00ffc4]/50 focus:ring-1 focus:ring-[#00ffc4]/20 transition-colors">
                                <option>Cloud Architecture</option>
                                <option>Infrastructure Review</option>
                                <option>DevOps Consulting</option>
                                <option>Full-time Opportunity</option>
                                <option>Other</option>
                            </select>
                        </div>
                        <div>
                            <label class="text-xs text-neutral-500 uppercase tracking-wider block mb-2">Message</label>
                            <textarea id="form-message" required rows="5" placeholder="Tell me about your project..." class="w-full px-4 py-3 rounded-lg bg-white/[0.03] border border-white/10 text-sm text-white placeholder-neutral-600 focus:outline-none focus:border-[#00ffc4]/50 focus:ring-1 focus:ring-[#00ffc4]/20 transition-colors resize-none"></textarea>
                        </div>
                        <button type="submit" class="w-full flex items-center justify-center gap-2 px-6 py-3.5 bg-[#00ffc4] text-black text-sm font-semibold rounded-lg hover:scale-[1.02] transition-all shadow-[0_0_20px_rgba(0,255,196,0.3)]">
                            <i data-lucide="send" class="w-4 h-4"></i>
                            Send Message
                        </button>
                    </form>
                </div>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="border-t border-white/5 py-12">
        <div class="max-w-7xl mx-auto px-6">
            <div class="flex flex-col md:flex-row items-center justify-between gap-6">
                <div class="flex items-center gap-2">
                    <div class="w-6 h-6 rounded bg-gradient-to-br from-[#00ffc4] to-[#047857] flex items-center justify-center">
                        <i data-lucide="cloud" class="w-3 h-3 text-black"></i>
                    </div>
                    <span class="font-['Oswald'] text-sm font-300 tracking-wide text-neutral-500">CLOUDFORGE</span>
                </div>
                <p class="text-xs text-neutral-600">© 2024 CloudForge. Built with passion and Terraform.</p>
                <div class="flex items-center gap-4">
                    <a href="#" class="text-neutral-600 hover:text-[#00ffc4] transition-colors"><i data-lucide="github" class="w-4 h-4"></i></a>
                    <a href="#" class="text-neutral-600 hover:text-[#00ffc4] transition-colors"><i data-lucide="linkedin" class="w-4 h-4"></i></a>
                    <a href="#" class="text-neutral-600 hover:text-[#00ffc4] transition-colors"><i data-lucide="twitter" class="w-4 h-4"></i></a>
                    <a href="#" class="text-neutral-600 hover:text-[#00ffc4] transition-colors"><i data-lucide="rss" class="w-4 h-4"></i></a>
                </div>
            </div>
        </div>
    </footer>

    <script>
        // Initialize Lucide icons
        lucide.createIcons();

        // ========== TYPING EFFECT ==========
        const commands = [
            'terraform apply --auto-approve',
            'kubectl get pods --all-namespaces',
            'aws ecs describe-clusters --cluster prod',
            'docker build -t cloudforge:latest .',
            'helm upgrade --install prod ./charts',
            'ansible-playbook deploy.yml -i inventory'
        ];
        let cmdIndex = 0, charIndex = 0, isDeleting = false;
        const typingEl = document.getElementById('typing-text');

        function typeEffect() {
            const current = commands[cmdIndex];
            if (!isDeleting) {
                typingEl.textContent = current.substring(0, charIndex + 1);
                charIndex++;
                if (charIndex === current.length) {
                    setTimeout(() => { isDeleting = true; typeEffect(); }, 2000);
                    return;
                }
            } else {
                typingEl.textContent = current.substring(0, charIndex - 1);
                charIndex--;
                if (charIndex === 0) {
                    isDeleting = false;
                    cmdIndex = (cmdIndex + 1) % commands.length;
                }
            }
            setTimeout(typeEffect, isDeleting ? 30 : 60);
        }
        setTimeout(typeEffect, 1000);

        // ========== COUNTER ANIMATION ==========
        function animateCounter(el, target, duration = 2000) {
            let start = 0;
            const step = target / (duration / 16);
            const timer = setInterval(() => {
                start += step;
                if (start >= target) { start = target; clearInterval(timer); }
                el.textContent = Math.floor(start) + (target > 10 ? '+' : '+');
            }, 16);
        }

        let statsAnimated = false;
        function checkStats() {
            if (statsAnimated) return;
            const el = document.getElementById('stat-years');
            const rect = el.getBoundingClientRect();
            if (rect.top < window.innerHeight * 0.9) {
                statsAnimated = true;
                animateCounter(document.getElementById('stat-years'), 5);
                animateCounter(document.getElementById('stat-projects'), 30);
                animateCounter(document.getElementById('stat-certs'), 5);
            }
        }

        // ========== SCROLL ANIMATIONS ==========
        const scrollObserver = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.classList.add('scroll-visible');
                    // Animate skill bars
                    entry.target.querySelectorAll('.skill-fill').forEach(bar => {
                        setTimeout(() => bar.classList.add('active'), 300);
                    });
                }
            });
        }, { threshold: 0.15, rootMargin: '0px 0px -10% 0px' });

        document.querySelectorAll('.scroll-hidden').forEach(el => scrollObserver.observe(el));

        // Stats check on scroll
        window.addEventListener('scroll', checkStats);
        checkStats();

        // ========== MOBILE MENU ==========
        const mobileToggle = document.getElementById('mobile-toggle');
        const mobileMenu = document.getElementById('mobile-menu');
        mobileToggle.addEventListener('click', () => {
            mobileMenu.classList.toggle('hidden');
        });
        document.querySelectorAll('.mobile-link').forEach(link => {
            link.addEventListener('click', () => mobileMenu.classList.add('hidden'));
        });

        // ========== PROJECT FILTER ==========
        const filterBtns = document.querySelectorAll('.filter-btn');
        const projectCards = document.querySelectorAll('.project-card');

        filterBtns.forEach(btn => {
            btn.addEventListener('click', () => {
                filterBtns.forEach(b => {
                    b.classList.remove('active');
                    b.style.borderColor = '';
                    b.style.color = '';
                    b.style.background = '';
                });
                btn.classList.add('active');
                btn.style.borderColor = 'rgba(0,255,196,0.3)';
                btn.style.color = '#fff';
                btn.style.background = 'rgba(0,255,196,0.05)';

                const filter = btn.dataset.filter;
                projectCards.forEach(card => {
                    const categories = card.dataset.category;
                    if (filter === 'all' || categories.includes(filter)) {
                        card.style.display = '';
                        card.style.opacity = '0';
                        card.style.transform = 'translateY(20px)';
                        setTimeout(() => {
                            card.style.transition = 'all 0.4s ease';
                            card.style.opacity = '1';
                            card.style.transform = 'translateY(0)';
                        }, 50);
                    } else {
                        card.style.transition = 'all 0.3s ease';
                        card.style.opacity = '0';
                        card.style.transform = 'translateY(20px)';
                        setTimeout(() => { card.style.display = 'none'; }, 300);
                    }
                });
            });
        });

        // Set initial active filter style
        const activeBtn = document.querySelector('.filter-btn.active');
        if (activeBtn) {
            activeBtn.style.borderColor = 'rgba(0,255,196,0.3)';
            activeBtn.style.color = '#fff';
            activeBtn.style.background = 'rgba(0,255,196,0.05)';
        }

        // ========== ACTIVE NAV LINK ==========
        const sections = document.querySelectorAll('section[id]');
        window.addEventListener('scroll', () => {
            let current = '';
            sections.forEach(section => {
                const top = section.offsetTop - 100;
                if (window.scrollY >= top) current = section.getAttribute('id');
            });
            document.querySelectorAll('.nav-link').forEach(link => {
                link.classList.remove('active');
                if (link.getAttribute('href') === '#' + current) {
                    link.classList.add('active');
                }
            });
        });

        // ========== TOAST NOTIFICATIONS ==========
        function showToast(message, type = 'success') {
            const container = document.getElementById('toast-container');
            const toast = document.createElement('div');
            const bgColor = type === 'success' ? 'bg-[#047857]' : 'bg-red-600';
            const icon = type === 'success' ? '✓' : '✕';
            toast.className = `toast-in flex items-center gap-3 px-5 py-3 rounded-xl ${bgColor} text-white text-sm shadow-lg`;
            toast.innerHTML = `<span class="w-5 h-5 rounded-full bg-white/20 flex items-center justify-center text-xs font-bold">${icon}</span> ${message}`;
            container.appendChild(toast);
            setTimeout(() => {
                toast.classList.remove('toast-in');
                toast.classList.add('toast-out');
                setTimeout(() => toast.remove(), 400);
            }, 4000);
        }

        // ========== CONTACT FORM ==========
        document.getElementById('contact-form').addEventListener('submit', (e) => {
            e.preventDefault();
            const name = document.getElementById('form-name').value;
            const email = document.getElementById('form-email').value;
            const message = document.getElementById('form-message').value;

            if (!name || !email || !message) {
                showToast('Please fill in all required fields.', 'error');
                return;
            }

            // Simulate sending
            const btn = e.target.querySelector('button[type="submit"]');
            const originalHTML = btn.innerHTML;
            btn.innerHTML = '<svg class="animate-spin w-4 h-4" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="10" stroke-dasharray="30 70"/></svg> Sending...';
            btn.disabled = true;

            setTimeout(() => {
                btn.innerHTML = originalHTML;
                btn.disabled = false;
                e.target.reset();
                showToast(`Thanks, ${name}! Your message has been sent successfully.`, 'success');
            }, 1500);
        });

        // ========== SMOOTH SCROLL ==========
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function(e) {
                e.preventDefault();
                const target = document.querySelector(this.getAttribute('href'));
                if (target) {
                    target.scrollIntoView({ behavior: 'smooth', block: 'start' });
                }
            });
        });

        // ========== NAV BACKGROUND ON SCROLL ==========
        const nav = document.querySelector('nav');
        window.addEventListener('scroll', () => {
            if (window.scrollY > 50) {
                nav.style.borderBottomColor = 'rgba(255,255,255,0.08)';
            } else {
                nav.style.borderBottomColor = 'rgba(255,255,255,0.03)';
            }
        });
    </script>
</body>
</html>
