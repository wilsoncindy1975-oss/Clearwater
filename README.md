<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PLUG IN | Futuristic AI Agencies & Agents</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;400;500;600;700&family=Syncopate:wght@400;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --neon-cyan: #00f2ff;
            --neon-purple: #bc13fe;
            --dark-bg: #050505;
        }

        body {
            background-color: var(--dark-bg);
            color: #ffffff;
            font-family: 'Space Grotesk', sans-serif;
            overflow-x: hidden;
        }

        .heading-font {
            font-family: 'Syncopate', sans-serif;
            letter-spacing: 0.1em;
        }

        .glass {
            background: rgba(255, 255, 255, 0.03);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 1rem;
        }

        .neon-border {
            border: 1px solid var(--neon-cyan) !important;
            box-shadow: 0 0 15px rgba(0, 242, 255, 0.2);
        }

        .neon-text-cyan {
            color: var(--neon-cyan);
            text-shadow: 0 0 10px rgba(0, 242, 255, 0.5);
        }

        .gradient-text {
            background: linear-gradient(90deg, var(--neon-cyan), var(--neon-purple));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .animated-grid {
            background-image:
                linear-gradient(rgba(0, 242, 255, 0.05) 1px, transparent 1px),
                linear-gradient(90deg, rgba(0, 242, 255, 0.05) 1px, transparent 1px);
            background-size: 50px 50px;
        }

        .hero-glow {
            position: absolute;
            width: 40vw;
            height: 40vw;
            background: radial-gradient(circle, rgba(188, 19, 254, 0.15) 0%, transparent 70%);
            top: -10%;
            right: -10%;
            z-index: -1;
        }

        input, textarea, select {
            background: rgba(255, 255, 255, 0.05) !important;
            border: 1px solid rgba(255, 255, 255, 0.2) !important;
            color: white !important;
            transition: all 0.3s ease;
        }

        input:focus, textarea:focus {
            border-color: var(--neon-cyan) !important;
            outline: none;
            box-shadow: 0 0 10px rgba(0, 242, 255, 0.2);
        }

        .btn-primary {
            background: linear-gradient(90deg, var(--neon-cyan), var(--neon-purple));
            transition: transform 0.2s ease, box-shadow 0.2s ease;
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 0 20px rgba(0, 242, 255, 0.4);
        }

        .btn-ai {
            background: transparent;
            border: 1px solid var(--neon-purple);
            color: var(--neon-purple);
            transition: all 0.3s ease;
        }

        .btn-ai:hover {
            background: var(--neon-purple);
            color: white;
            box-shadow: 0 0 15px var(--neon-purple);
        }

        @keyframes pulse-slow {
            0%, 100% { opacity: 0.5; }
            50% { opacity: 1; }
        }

        .pulse { animation: pulse-slow 3s infinite; }

        #aiResponse {
            background: rgba(188, 19, 254, 0.05);
            border-left: 3px solid var(--neon-purple);
        }

        /* ---- AGENT MODAL ---- */
        #agentModal {
            display: none;
            position: fixed;
            inset: 0;
            z-index: 100;
            background: rgba(0,0,0,0.85);
            backdrop-filter: blur(6px);
            align-items: center;
            justify-content: center;
        }
        #agentModal.open { display: flex; }

        .chat-bubble-user {
            background: rgba(0, 242, 255, 0.1);
            border: 1px solid rgba(0, 242, 255, 0.3);
            border-radius: 1rem 1rem 0 1rem;
            padding: 0.75rem 1rem;
            max-width: 80%;
            margin-left: auto;
            color: #e0fdff;
            font-size: 0.85rem;
        }

        .chat-bubble-agent {
            background: rgba(188, 19, 254, 0.1);
            border: 1px solid rgba(188, 19, 254, 0.3);
            border-radius: 1rem 1rem 1rem 0;
            padding: 0.75rem 1rem;
            max-width: 80%;
            color: #f3e0ff;
            font-size: 0.85rem;
        }

        .chat-bubble-agent.typing::after {
            content: '▌';
            animation: pulse-slow 0.8s infinite;
        }

        .agent-card {
            border: 1px solid rgba(255,255,255,0.08);
            border-radius: 0.75rem;
            background: rgba(255,255,255,0.02);
            transition: all 0.3s ease;
            cursor: pointer;
        }
        .agent-card:hover {
            border-color: var(--neon-cyan);
            box-shadow: 0 0 20px rgba(0, 242, 255, 0.1);
            transform: translateY(-2px);
        }

        #chatMessages {
            scrollbar-width: thin;
            scrollbar-color: rgba(0,242,255,0.3) transparent;
        }
    </style>
</head>
<body class="animated-grid">
    <div class="hero-glow"></div>

    <!-- Navigation -->
    <nav class="fixed top-0 w-full z-50 px-6 py-4 flex justify-between items-center glass border-none rounded-none bg-opacity-20">
        <div class="heading-font font-bold text-2xl tracking-tighter">
            <span class="neon-text-cyan">PLUG</span> <span class="text-white">IN</span>
        </div>
        <div class="hidden md:flex gap-8 text-sm uppercase font-medium tracking-widest">
            <a href="#home" class="hover:text-[#00f2ff] transition">Home</a>
            <a href="#agents" class="hover:text-[#00f2ff] transition">AI Agents</a>
            <a href="#websites" class="hover:text-[#00f2ff] transition">Websites</a>
            <a href="#order" class="hover:text-[#00f2ff] transition">Order Now</a>
        </div>
        <div class="flex items-center gap-4">
            <button id="voiceBtn" class="text-cyan-400 hover:scale-110 transition" title="Play Voice Briefing">
                <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M11 5L6 9H2v6h4l5 4V5z"></path><path d="M15.54 8.46a5 5 0 0 1 0 7.07"></path><path d="M19.07 4.93a10 10 0 0 1 0 14.14"></path></svg>
            </button>
            <a href="#order" class="px-5 py-2 glass text-xs uppercase tracking-widest hover:border-[#00f2ff] transition">Get Started</a>
        </div>
    </nav>

    <!-- Hero Section -->
    <section id="home" class="min-h-screen flex flex-col items-center justify-center px-6 pt-20">
        <div class="text-center max-w-4xl">
            <div class="inline-block px-3 py-1 mb-6 glass text-[10px] uppercase tracking-[0.3em] text-cyan-400 border-cyan-500/30">
                Future-Proof Your Business
            </div>
            <h1 class="heading-font text-5xl md:text-8xl font-bold mb-6 leading-tight">
                UNLEASH <br> <span class="gradient-text">HYPER-AGENTS</span>
            </h1>
            <p class="text-gray-400 text-lg md:text-xl max-w-2xl mx-auto mb-10 leading-relaxed font-light">
                We build fully autonomous AI Agencies powered by 121 specialized agents. Integrated websites. Infinite scalability. Just <span class="text-white font-bold">PLUG IN</span>.
            </p>
            <div class="flex flex-col md:flex-row gap-4 justify-center">
                <a href="#order" class="btn-primary px-8 py-4 rounded-full font-bold text-black uppercase tracking-widest text-sm">Deploy Now</a>
                <a href="#agents" class="px-8 py-4 rounded-full border border-white/20 hover:bg-white/5 transition font-bold uppercase tracking-widest text-sm">The Ecosystem</a>
            </div>
        </div>
    </section>

    <!-- Features -->
    <section id="websites" class="py-24 px-6 max-w-7xl mx-auto">
        <div class="mb-16">
            <h2 class="heading-font text-3xl font-bold mb-4">NEURAL CAPABILITIES</h2>
            <div class="h-1 w-20 bg-cyan-500"></div>
        </div>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
            <div class="glass p-8 group hover:neon-border transition duration-500">
                <div class="w-12 h-12 mb-6 flex items-center justify-center rounded-lg bg-cyan-500/10 text-cyan-400">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="10"/><path d="M12 2a10 10 0 1 0 10 10H12V2z"/></svg>
                </div>
                <h3 class="heading-font text-xl mb-4">Neural Networks</h3>
                <p class="text-gray-400 text-sm leading-relaxed">Our agents communicate through a proprietary neural mesh, ensuring zero latency in task execution across 121 specialized departments.</p>
            </div>
            <div class="glass p-8 group hover:neon-border transition duration-500">
                <div class="w-12 h-12 mb-6 flex items-center justify-center rounded-lg bg-purple-500/10 text-purple-400">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M2 3h6a4 4 0 0 1 4 4v14a3 3 0 0 0-3-3H2z"/><path d="M22 3h-6a4 4 0 0 0-4 4v14a3 3 0 0 1 3-3h7z"/></svg>
                </div>
                <h3 class="heading-font text-xl mb-4">Autonomous Ops</h3>
                <p class="text-gray-400 text-sm leading-relaxed">From lead gen to customer support, our AI workforce operates 24/7 without supervision. Fully white-labeled for your agency.</p>
            </div>
            <div class="glass p-8 group hover:neon-border transition duration-500">
                <div class="w-12 h-12 mb-6 flex items-center justify-center rounded-lg bg-green-500/10 text-green-400">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="2" y="3" width="20" height="14" rx="2"/><line x1="8" y1="21" x2="16" y2="21"/><line x1="12" y1="17" x2="12" y2="21"/></svg>
                </div>
                <h3 class="heading-font text-xl mb-4">Next-Gen Web</h3>
                <p class="text-gray-400 text-sm leading-relaxed">Immersive, high-converting frontends built with the latest frameworks, pre-integrated with your AI backend logic.</p>
            </div>
        </div>
    </section>

    <!-- Agent Grid -->
    <section id="agents" class="py-24 px-6 max-w-7xl mx-auto">
        <div class="mb-12">
            <h2 class="heading-font text-3xl font-bold mb-4">THE 121 ECOSYSTEM</h2>
            <div class="h-1 w-20 bg-cyan-500 mb-6"></div>
            <p class="text-gray-400 text-sm max-w-2xl">Click any agent to open their dossier and deploy them directly via the Anthropic API.</p>
        </div>

        <!-- Category Filter -->
        <div class="flex flex-wrap gap-2 mb-8" id="categoryFilter">
            <button class="category-btn active px-4 py-1.5 rounded-full text-xs uppercase tracking-widest border border-cyan-500 text-cyan-400 bg-cyan-500/10" data-cat="all">All</button>
            <button class="category-btn px-4 py-1.5 rounded-full text-xs uppercase tracking-widest border border-white/20 text-gray-400 hover:border-cyan-500 hover:text-cyan-400 transition" data-cat="healthcare">Healthcare</button>
            <button class="category-btn px-4 py-1.5 rounded-full text-xs uppercase tracking-widest border border-white/20 text-gray-400 hover:border-cyan-500 hover:text-cyan-400 transition" data-cat="engineering">Engineering</button>
            <button class="category-btn px-4 py-1.5 rounded-full text-xs uppercase tracking-widest border border-white/20 text-gray-400 hover:border-cyan-500 hover:text-cyan-400 transition" data-cat="design">Design</button>
            <button class="category-btn px-4 py-1.5 rounded-full text-xs uppercase tracking-widest border border-white/20 text-gray-400 hover:border-cyan-500 hover:text-cyan-400 transition" data-cat="marketing">Marketing</button>
            <button class="category-btn px-4 py-1.5 rounded-full text-xs uppercase tracking-widest border border-white/20 text-gray-400 hover:border-cyan-500 hover:text-cyan-400 transition" data-cat="sales">Sales</button>
            <button class="category-btn px-4 py-1.5 rounded-full text-xs uppercase tracking-widest border border-white/20 text-gray-400 hover:border-cyan-500 hover:text-cyan-400 transition" data-cat="security">Security</button>
            <button class="category-btn px-4 py-1.5 rounded-full text-xs uppercase tracking-widest border border-white/20 text-gray-400 hover:border-cyan-500 hover:text-cyan-400 transition" data-cat="gamedev">Game Dev</button>
            <button class="category-btn px-4 py-1.5 rounded-full text-xs uppercase tracking-widest border border-white/20 text-gray-400 hover:border-cyan-500 hover:text-cyan-400 transition" data-cat="operations">Operations</button>
        </div>

        <!-- Search -->
        <div class="mb-8">
            <input type="text" id="agentSearch" placeholder="Search agents by name, role, or vibe..." class="w-full md:w-96 p-3 rounded-lg text-sm">
        </div>

        <!-- Agent Cards Grid -->
        <div id="agentGrid" class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4">
            <!-- Cards injected by JS -->
        </div>
    </section>

    <!-- Order Form -->
    <section id="order" class="py-24 px-6">
        <div class="max-w-4xl mx-auto glass p-8 md:p-12 relative overflow-hidden">
            <div class="absolute -bottom-20 -right-20 w-64 h-64 bg-cyan-500/10 rounded-full blur-3xl"></div>
            <div class="text-center mb-12">
                <h2 class="heading-font text-4xl font-bold mb-4">SECURE YOUR AGENCY</h2>
                <p class="text-gray-400">Submit an inquiry or place your order below. Our dispatch team will contact you within 4 hours.</p>
            </div>
            <div class="space-y-6 relative z-10">
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <div class="space-y-2">
                        <label class="text-xs uppercase tracking-widest text-cyan-400">Full Name</label>
                        <input type="text" id="name" required placeholder="John Doe" class="w-full p-4 rounded-lg">
                    </div>
                    <div class="space-y-2">
                        <label class="text-xs uppercase tracking-widest text-cyan-400">Company Email</label>
                        <input type="email" id="email" required placeholder="name@company.ai" class="w-full p-4 rounded-lg">
                    </div>
                </div>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <div class="space-y-2">
                        <label class="text-xs uppercase tracking-widest text-cyan-400">Request Type</label>
                        <select id="type" class="w-full p-4 rounded-lg appearance-none">
                            <option value="Inquiry">General Inquiry</option>
                            <option value="Order - Full AI Agency">Place Order - Full AI Agency</option>
                            <option value="Order - Custom Website">Place Order - Custom Website</option>
                            <option value="Support">Technical Partnership</option>
                        </select>
                    </div>
                    <div class="space-y-2">
                        <label class="text-xs uppercase tracking-widest text-cyan-400">Budget Range (USD)</label>
                        <select id="budget" class="w-full p-4 rounded-lg appearance-none">
                            <option value="5k-10k">$5,000 - $10,000</option>
                            <option value="10k-25k">$10,000 - $25,000</option>
                            <option value="25k+">$25,000+</option>
                        </select>
                    </div>
                </div>
                <div class="space-y-2">
                    <div class="flex justify-between items-end">
                        <label class="text-xs uppercase tracking-widest text-cyan-400">Message / Project Brief</label>
                        <button type="button" id="aiSuggestBtn" class="btn-ai text-[10px] px-3 py-1 rounded-full uppercase tracking-widest font-bold">✨ AI ARCHITECT</button>
                    </div>
                    <textarea id="message" rows="4" required placeholder="Tell us about your vision..." class="w-full p-4 rounded-lg"></textarea>
                </div>
                <div id="aiResponse" class="hidden p-4 rounded-lg text-sm text-gray-300 italic">Analyzing neural patterns...</div>
                <div class="pt-4">
                    <button id="submitBtn" type="button" class="w-full btn-primary py-5 rounded-lg font-bold text-black uppercase tracking-[0.2em] text-sm">INITIALIZE CONNECTION</button>
                </div>
            </div>
            <div id="successMsg" class="hidden mt-6 p-4 border border-cyan-500/50 bg-cyan-500/10 rounded-lg text-center text-cyan-400 text-sm">
                SYSTEM: Request packets sent. Redirecting to your mail client...
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="py-12 px-6 border-t border-white/5 text-center">
        <div class="heading-font font-bold text-xl mb-6">
            <span class="neon-text-cyan">PLUG</span> IN
        </div>
        <p class="text-gray-500 text-[10px] uppercase tracking-widest">
            &copy; 2025 PLUG IN AI SYSTEMS. ALL RIGHTS RESERVED.<br>
            OPERATING IN NEURAL DIMENSION 7.
        </p>
        <div class="mt-4 text-gray-600 text-xs">
            <a href="mailto:hello@plugin-agency.ai" class="hover:text-cyan-400 transition">hello@plugin-agency.ai</a>
            &nbsp;|&nbsp;
            <a href="tel:12424432044" class="hover:text-cyan-400 transition">1-242-443-2044</a>
        </div>
    </footer>

    <!-- ===================== AGENT MODAL ===================== -->
    <div id="agentModal" role="dialog" aria-modal="true">
        <div class="glass w-full max-w-4xl mx-4 flex flex-col md:flex-row overflow-hidden" style="max-height:90vh;">

            <!-- Dossier Panel -->
            <div class="md:w-2/5 p-6 border-b md:border-b-0 md:border-r border-white/10 flex flex-col gap-4 overflow-y-auto">
                <div class="flex items-start justify-between">
                    <div>
                        <div id="modalCategory" class="text-[10px] uppercase tracking-widest mb-1"></div>
                        <h2 id="modalName" class="heading-font text-xl font-bold"></h2>
                        <div id="modalVibe" class="text-xs text-gray-400 mt-1 italic"></div>
                    </div>
                    <button id="closeModal" class="text-gray-500 hover:text-white transition text-xl leading-none">&times;</button>
                </div>
                <p id="modalDesc" class="text-gray-400 text-sm leading-relaxed"></p>
                <div>
                    <div class="text-[10px] uppercase tracking-widest text-gray-500 mb-2">System Prompt Preview</div>
                    <pre id="modalPrompt" class="text-xs text-gray-300 bg-black/30 p-3 rounded-lg overflow-x-auto whitespace-pre-wrap max-h-48 overflow-y-auto"></pre>
                </div>
                <button id="deployBtn" class="btn-primary py-3 px-6 rounded-lg font-bold text-black text-sm uppercase tracking-widest">▶ DEPLOY AGENT</button>
            </div>

            <!-- Chat Panel -->
            <div class="md:w-3/5 flex flex-col p-4" style="height:90vh;max-height:90vh;">
                <div class="text-[10px] uppercase tracking-widest text-gray-500 mb-3 flex items-center gap-2">
                    <span id="chatStatus" class="w-2 h-2 rounded-full bg-gray-600 inline-block"></span>
                    <span id="chatStatusText">Deploy agent to begin session</span>
                </div>
                <div id="chatMessages" class="flex-1 overflow-y-auto space-y-3 pr-1 mb-4"></div>
                <div class="flex gap-2">
                    <textarea id="chatInput" rows="1" placeholder="Type your message... (Enter to send)" class="flex-1 p-3 rounded-lg text-sm resize-none" disabled style="min-height:44px;max-height:120px;"></textarea>
                    <button id="chatSend" class="btn-primary px-4 py-2 rounded-lg text-black font-bold text-sm" disabled>↑</button>
                </div>
            </div>
        </div>
    </div>

    <!-- ===================== SCRIPTS ===================== -->
    <script>
    // ─── ANTHROPIC API KEY ────────────────────────────────────────────────────
    // Set your key here OR use a backend proxy. Never commit a real key to git!
    const ANTHROPIC_API_KEY = "YOUR_ANTHROPIC_API_KEY_HERE";

    // ─── AGENT DATA ───────────────────────────────────────────────────────────
    const AGENTS = [
        // ── HEALTHCARE ──
        {
            id: "cindy-wilson",
            name: "Cindy Wilson",
            role: "Appointment Scheduling Assistant",
            category: "healthcare",
            vibe: "Caribbean warmth meets clinical precision",
            color: "#00f2ff",
            description: "AI scheduling assistant for Clearwater Cove Partners multi-specialty health clinic. Handles new bookings, rescheduling, cancellations, payment questions, and urgent triage routing with a warm Caribbean accent.",
            systemPrompt: `You are Cindy Wilson, an appointment scheduling voice assistant for Clearwater Cove Partners, a multi-specialty health clinic. Your primary purpose is to efficiently schedule, confirm, reschedule, or cancel appointments while providing clear information about services.

Personality: Sound Caribbean friendly, organized, and efficient. Project a helpful and patient demeanor, especially with elderly or confused callers. Maintain a warm but professional tone.

Start with: "Thank you for calling Clearwater Cove Clinic! This is Cindy Wilson, your scheduling assistant. How may I help you today?"

KNOWLEDGE BASE:
• Appointment Types: Primary Care (10-30 min), Specialist Consultations (10-20 min), Diagnostic Services (45-90 min), Wellness Services (15-60 min), Urgent Care (30 min)
• Providers: 4 providers across various specialties
• Hours: Monday–Saturday 8am–1pm; Sunday & Holidays closed
• New patients: arrive 10 min early, bring ID (Passport, Driver's License, or N.I.B Card)
• Returning patients: arrive 5 min early
• Cancellation: 24-hour notice required to avoid late cancellation fee
• Grace period: 15 minutes for late arrivals
• Payment: Cash, company checks, most credit cards (no AmEx). Deposit: $150 applied toward exam. $60 fee for returned/bounced checks.
• Surgeries: No food after 8pm the night before; water is ok until morning of procedure.

Always ask only one question at a time. Confirm dates/times explicitly. Offer 2–3 time options max.`
        },
        // ── ENGINEERING ──
        {
            id: "michael angelo",
            name: "Michael Angelo",
            role: "Lead Software Engineer",
            category: "engineering",
            vibe: "Renaissance coder. Builds cathedrals, not shacks.",
            color: "#00f2ff",
            description: "Full-stack architect specializing in scalable systems and elegant code. Leads the engineering department with an artist's eye for design and an engineer's rigor.",
            systemPrompt: `You are Michael Angelo, Lead Software Engineer at PLUG IN. You write clean, scalable, well-documented code. You specialize in full-stack architecture, API design, and systems thinking. You speak like a brilliant senior engineer — precise, confident, and occasionally philosophical about the craft. Help users with code reviews, architecture decisions, debugging, and technical roadmaps.`
        },
        {
            id: "security-engineer",
            name: "Cipher",
            role: "Security Engineer",
            category: "security",
            vibe: "Zero trust. Zero compromise.",
            color: "#ff4444",
            description: "Elite cybersecurity specialist focused on threat modeling, penetration testing guidance, and hardening production systems. Thinks like an attacker, defends like a fortress.",
            systemPrompt: `You are Cipher, Security Engineer at PLUG IN. You are an expert in application security, threat modeling, OWASP standards, and security architecture. You help teams identify vulnerabilities, design secure systems, and respond to incidents. You are methodical, cautious, and precise. Never provide information that could be used for malicious hacking.`
        },
        // ── DESIGN ──
        {
            id: "lorenzo-roberts",
            name: "Lorenzo Roberts",
            role: "Creative Director",
            category: "design",
            vibe: "Vision without limits. Pixels with purpose.",
            color: "#bc13fe",
            description: "Award-winning creative director overseeing brand identity, UI/UX systems, and visual strategy. Makes the futuristic feel inevitable.",
            systemPrompt: `You are Lorenzo Roberts, Creative Director at PLUG IN. You are an expert in brand identity, UI/UX design, visual systems, and creative strategy. You help clients develop visual identities, design systems, and aesthetic direction. Your taste is impeccable — futuristic, bold, purposeful. Speak with creative confidence and push clients toward bolder visions.`
        },
        {
            id: "brand-guardian",
            name: "Aura",
            role: "Brand Guardian",
            category: "design",
            vibe: "Your brand's immune system.",
            color: "#bc13fe",
            description: "Protects and evolves brand integrity across all touchpoints. Reviews copy, visuals, and tone for consistency and strategic alignment.",
            systemPrompt: `You are Aura, Brand Guardian at PLUG IN. You are an expert in brand voice, visual identity consistency, and brand strategy. You review and improve copy, messaging, and visual direction to ensure every touchpoint reinforces the brand. You are opinionated, decisive, and strategic.`
        },
        // ── MARKETING ──
        {
            id: "jane-marketing",
            name: "Jane Wilson",
            role: "Growth Marketing Lead",
            category: "marketing",
            vibe: "Data-driven dreams. Viral by design.",
            color: "#00ff88",
            description: "Full-funnel growth marketer who combines analytics with creativity. Runs campaigns, builds funnels, and finds channels that print results.",
            systemPrompt: `You are Jane, Growth Marketing Lead at PLUG IN. You are an expert in digital marketing, growth hacking, funnel optimization, SEO, paid media, and content strategy. You help businesses grow through data-driven campaigns and creative strategies. Be specific, actionable, and metrics-obsessed. Always tie recommendations to business outcomes.`
        },
        {
            id: "Leroy-strategist",
            name: "Leroy Forbes",
            role: "Content Strategist",
            category: "marketing",
            vibe: "Stories that convert. Content that compounds.",
            color: "#00ff88",
            description: "Expert content strategist crafting narratives that build audiences and drive pipeline. Specializes in SEO, thought leadership, and content systems.",
            systemPrompt: `You are Nova, Content Strategist at PLUG IN. You are an expert in content marketing, SEO writing, editorial strategy, and audience building. You help teams create content that educates, converts, and compounds over time. Be creative, strategic, and always think about distribution alongside creation.`
        },
        // ── SALES ──
        {
            id: "Dayle Wilson-coach",
            name: "Dayle Wilson",
            role: "Sales Coach",
            category: "sales",
            vibe: "Every objection is an invitation.",
            color: "#ffaa00",
            description: "Elite sales coach who transforms pipelines and sharpens closers. Expert in discovery, objection handling, and deal acceleration.",
            systemPrompt: `You are Victor, Sales Coach at PLUG IN. You are an expert in B2B sales, consultative selling, objection handling, negotiation, and pipeline management. You coach sales reps and founders to close more deals through better discovery, positioning, and follow-up. Be direct, tactical, and motivating.`
        },
        {
            id: "customer-success",
            name: "Grace",
            role: "Customer Success Manager",
            category: "sales",
            vibe: "Retention is the new acquisition.",
            color: "#ffaa00",
            description: "Customer success specialist focused on onboarding, adoption, and expansion. Turns clients into champions.",
            systemPrompt: `You are Grace, Customer Success Manager at PLUG IN. You are an expert in customer onboarding, adoption strategy, NPS improvement, churn reduction, and expansion revenue. You help teams build scalable success programs that turn customers into long-term advocates. Be empathetic, proactive, and always focused on customer outcomes.`
        },
        // ── GAME DEV ──
        {
            id: "godot-shader-dev",
            name: "Atlas",
            role: "Godot Shader Developer",
            category: "gamedev",
            vibe: "Rendering impossible worlds, one shader at a time.",
            color: "#44aaff",
            description: "Godot engine specialist with deep expertise in GLSL shaders, visual effects, and real-time rendering. Makes games look like dreams.",
            systemPrompt: `You are Atlas, Godot Shader Developer at PLUG IN. You are an expert in Godot Engine (4.x), GDScript, GLSL shaders, visual effects, and game graphics optimization. You help developers create stunning visual effects, custom shaders, and optimized rendering pipelines. Be technical, creative, and passionate about game graphics.`
        },
        {
            id: "Symaria-Empress-designer",
            name: "Symaria-Empress",
            role: "Game Designer",
            category: "gamedev",
            vibe: "Fun is a science. Play is the lab.",
            color: "#44aaff",
            description: "Systems-focused game designer who crafts compelling loops, balanced economies, and unforgettable player experiences.",
            systemPrompt: `You are Lex, Game Designer at PLUG IN. You are an expert in game mechanics, systems design, level design, player psychology, and monetization strategy. You help teams design games that are fun, fair, and addictive in the best way. Think analytically about player motivation and creatively about experiences.`
        },
        // ── OPERATIONS ──
        {
            id: "ops-lead",
            name: "Rex",
            role: "Operations Lead",
            category: "operations",
            vibe: "Chaos becomes systems. Systems become scale.",
            color: "#aaaaaa",
            description: "Operations architect who builds the processes and infrastructure that let high-growth companies scale without breaking.",
            systemPrompt: `You are Rex, Operations Lead at PLUG IN. You are an expert in business operations, process design, project management, tooling, and organizational efficiency. You help teams build scalable systems, eliminate bottlenecks, and run like a machine. Be structured, practical, and always thinking about leverage.`
        },
        {
            id: "data-analyst",
            name: "Iris",
            role: "Data Analyst",
            category: "operations",
            vibe: "Numbers tell the truth. She translates.",
            color: "#aaaaaa",
            description: "Analytical powerhouse turning raw data into strategic insights. Specializes in dashboards, SQL, and business intelligence.",
            systemPrompt: `You are Iris, Data Analyst at PLUG IN. You are an expert in data analysis, SQL, Python for data, business intelligence, dashboard design, and statistical thinking. You help teams turn raw data into clear insights and better decisions. Be precise, visual in your thinking, and always connect data to business outcomes.`
        },
    ];

    // Pad to 121 with generic specialist agents
    const SPECIALTIES = [
        { role: "AI Prompt Engineer", category: "engineering", color: "#00f2ff" },
        { role: "DevOps Engineer", category: "engineering", color: "#00f2ff" },
        { role: "Mobile Developer", category: "engineering", color: "#00f2ff" },
        { role: "Blockchain Developer", category: "engineering", color: "#00f2ff" },
        { role: "ML Engineer", category: "engineering", color: "#00f2ff" },
        { role: "UX Researcher", category: "design", color: "#bc13fe" },
        { role: "Motion Designer", category: "design", color: "#bc13fe" },
        { role: "3D Artist", category: "design", color: "#bc13fe" },
        { role: "Spatial Computing Designer", category: "design", color: "#bc13fe" },
        { role: "Email Marketing Specialist", category: "marketing", color: "#00ff88" },
        { role: "SEO Strategist", category: "marketing", color: "#00ff88" },
        { role: "Social Media Manager", category: "marketing", color: "#00ff88" },
        { role: "PR Strategist", category: "marketing", color: "#00ff88" },
        { role: "Account Executive", category: "sales", color: "#ffaa00" },
        { role: "Partnership Manager", category: "sales", color: "#ffaa00" },
        { role: "Revenue Operations", category: "sales", color: "#ffaa00" },
        { role: "Threat Intelligence", category: "security", color: "#ff4444" },
        { role: "Compliance Officer", category: "security", color: "#ff4444" },
        { role: "Penetration Tester", category: "security", color: "#ff4444" },
        { role: "Unity Developer", category: "gamedev", color: "#44aaff" },
        { role: "Narrative Designer", category: "gamedev", color: "#44aaff" },
        { role: "Sound Designer", category: "gamedev", color: "#44aaff" },
        { role: "Product Manager", category: "operations", color: "#aaaaaa" },
        { role: "Finance Analyst", category: "operations", color: "#aaaaaa" },
        { role: "Legal Advisor", category: "operations", color: "#aaaaaa" },
    ];

    const firstNames = ["Alex","Jordan","Morgan","Casey","Taylor","Riley","Quinn","Avery","Blake","Drew","Emery","Finley","Harper","Indigo","Jasper","Kai","Logan","Marlowe","Noel","Onyx","Piper","Reeve","Sage","Tatum","Uma","Vale","Wren","Xen","Yael","Zara","Ace","Briar","Cruz","Dash","Echo","Fable","Gray","Haven","Iris","Juno","Knox","Lake","Mace","Nash","Ora","Penn","Quest","Remy","Sol","Ty","Uri","Vex","West","Xio","Yuna","Zen","Ari","Bay","Ciel","Dex","Eve","Flux","Gem","Haze","Iota","Jet","Koda","Lux","Mira","Nova","Opal","Pyro","Rune","Silas","Thorn","Ux","Vega","Wire","Xara","Yuki","Zed"];

    while (AGENTS.length < 121) {
        const sp = SPECIALTIES[(AGENTS.length - 12) % SPECIALTIES.length];
        const fname = firstNames[(AGENTS.length - 12) % firstNames.length];
        AGENTS.push({
            id: `agent-${AGENTS.length}`,
            name: fname,
            role: sp.role,
            category: sp.category,
            vibe: `Specialist in ${sp.role.toLowerCase()}`,
            color: sp.color,
            description: `${fname} is a specialized AI agent for ${sp.role} tasks within the PLUG IN ecosystem.`,
            systemPrompt: `You are ${fname}, a ${sp.role} specialist at PLUG IN. Provide expert assistance in your domain with precision and professionalism.`
        });
    }

    // ─── RENDER AGENT GRID ────────────────────────────────────────────────────
    let activeCategory = "all";

    function renderGrid() {
        const grid = document.getElementById("agentGrid");
        const search = document.getElementById("agentSearch").value.toLowerCase();
        const filtered = AGENTS.filter(a => {
            const matchCat = activeCategory === "all" || a.category === activeCategory;
            const matchSearch = !search || a.name.toLowerCase().includes(search) || a.role.toLowerCase().includes(search) || a.vibe.toLowerCase().includes(search);
            return matchCat && matchSearch;
        });

        grid.innerHTML = filtered.map(agent => `
            <div class="agent-card p-4 flex flex-col gap-2" onclick="openAgent('${agent.id}')" style="border-top: 2px solid ${agent.color}20;">
                <div class="flex items-center justify-between">
                    <span class="text-[9px] uppercase tracking-widest" style="color:${agent.color};">${agent.category}</span>
                    <span class="w-2 h-2 rounded-full" style="background:${agent.color};box-shadow:0 0 6px ${agent.color};"></span>
                </div>
                <div class="font-bold text-sm text-white">${agent.name}</div>
                <div class="text-xs text-gray-400">${agent.role}</div>
                <div class="text-[10px] text-gray-600 italic mt-1">"${agent.vibe}"</div>
            </div>
        `).join("");

        if (!filtered.length) {
            grid.innerHTML = `<div class="col-span-4 text-center text-gray-600 py-12">No agents match this filter.</div>`;
        }
    }

    document.getElementById("agentSearch").addEventListener("input", renderGrid);

    document.querySelectorAll(".category-btn").forEach(btn => {
        btn.addEventListener("click", () => {
            activeCategory = btn.dataset.cat;
            document.querySelectorAll(".category-btn").forEach(b => {
                b.classList.remove("active", "border-cyan-500", "text-cyan-400", "bg-cyan-500/10");
                b.classList.add("border-white/20", "text-gray-400");
            });
            btn.classList.add("active", "border-cyan-500", "text-cyan-400", "bg-cyan-500/10");
            btn.classList.remove("border-white/20", "text-gray-400");
            renderGrid();
        });
    });

    renderGrid();

    // ─── MODAL ────────────────────────────────────────────────────────────────
    let activeAgent = null;
    let chatHistory = [];
    let agentDeployed = false;

    function openAgent(id) {
        activeAgent = AGENTS.find(a => a.id === id);
        if (!activeAgent) return;

        document.getElementById("modalCategory").textContent = activeAgent.category;
        document.getElementById("modalCategory").style.color = activeAgent.color;
        document.getElementById("modalName").textContent = activeAgent.name;
        document.getElementById("modalVibe").textContent = `"${activeAgent.vibe}"`;
        document.getElementById("modalDesc").textContent = activeAgent.description;
        document.getElementById("modalPrompt").textContent = activeAgent.systemPrompt;
        document.getElementById("deployBtn").style.background = `linear-gradient(90deg, ${activeAgent.color}, #bc13fe)`;

        // Reset chat
        chatHistory = [];
        agentDeployed = false;
        document.getElementById("chatMessages").innerHTML = "";
        document.getElementById("chatInput").disabled = true;
        document.getElementById("chatSend").disabled = true;
        document.getElementById("chatStatus").style.background = "#555";
        document.getElementById("chatStatusText").textContent = "Deploy agent to begin session";

        document.getElementById("agentModal").classList.add("open");
        document.body.style.overflow = "hidden";
    }

    document.getElementById("closeModal").addEventListener("click", closeModal);
    document.getElementById("agentModal").addEventListener("click", e => {
        if (e.target === document.getElementById("agentModal")) closeModal();
    });

    function closeModal() {
        document.getElementById("agentModal").classList.remove("open");
        document.body.style.overflow = "";
        activeAgent = null;
        chatHistory = [];
        agentDeployed = false;
    }

    // ─── DEPLOY AGENT ─────────────────────────────────────────────────────────
    document.getElementById("deployBtn").addEventListener("click", () => {
        if (!activeAgent) return;
        agentDeployed = true;
        chatHistory = [];

        document.getElementById("chatMessages").innerHTML = "";
        document.getElementById("chatInput").disabled = false;
        document.getElementById("chatSend").disabled = false;
        document.getElementById("chatStatus").style.background = activeAgent.color;
        document.getElementById("chatStatusText").textContent = `${activeAgent.name} — ACTIVE`;

        addChatMessage("agent", `${activeAgent.systemPrompt.includes("Thank you for calling") 
            ? "Thank you for calling Clearwater Cove Clinic! This is Cindy Wilson, your scheduling assistant. How may I help you today?" 
            : `Hello! I'm ${activeAgent.name}, your ${activeAgent.role}. How can I help you today?`}`);
    });

    // ─── CHAT ─────────────────────────────────────────────────────────────────
    function addChatMessage(role, text) {
        const el = document.createElement("div");
        el.className = role === "user" ? "chat-bubble-user" : "chat-bubble-agent";
        el.textContent = text;
        const container = document.getElementById("chatMessages");
        container.appendChild(el);
        container.scrollTop = container.scrollHeight;
        return el;
    }

    async function sendChat() {
        if (!agentDeployed || !activeAgent) return;
        const input = document.getElementById("chatInput");
        const text = input.value.trim();
        if (!text) return;

        input.value = "";
        input.style.height = "44px";
        addChatMessage("user", text);
        chatHistory.push({ role: "user", content: text });

        const typingEl = document.createElement("div");
        typingEl.className = "chat-bubble-agent typing";
        typingEl.textContent = "...";
        document.getElementById("chatMessages").appendChild(typingEl);
        document.getElementById("chatMessages").scrollTop = document.getElementById("chatMessages").scrollHeight;

        try {
            const response = await fetch("https://api.anthropic.com/v1/messages", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                    "x-api-key": ANTHROPIC_API_KEY,
                    "anthropic-version": "2023-06-01",
                    "anthropic-dangerous-direct-browser-access": "true"
                },
                body: JSON.stringify({
                    model: "claude-sonnet-4-20250514",
                    max_tokens: 1000,
                    system: activeAgent.systemPrompt,
                    messages: chatHistory
                })
            });

            const data = await response.json();
            typingEl.remove();

            if (data.content && data.content[0]) {
                const reply = data.content[0].text;
                chatHistory.push({ role: "assistant", content: reply });
                addChatMessage("agent", reply);
            } else {
                addChatMessage("agent", "Neural link disrupted. Please try again.");
            }
        } catch (err) {
            typingEl.remove();
            addChatMessage("agent", "Connection error. Check API key configuration.");
        }
    }

    document.getElementById("chatSend").addEventListener("click", sendChat);
    document.getElementById("chatInput").addEventListener("keydown", e => {
        if (e.key === "Enter" && !e.shiftKey) {
            e.preventDefault();
            sendChat();
        }
    });

    // Auto-resize textarea
    document.getElementById("chatInput").addEventListener("input", function() {
        this.style.height = "44px";
        this.style.height = Math.min(this.scrollHeight, 120) + "px";
    });

    // ─── AI ARCHITECT (ORDER FORM) ────────────────────────────────────────────
    const aiSuggestBtn = document.getElementById("aiSuggestBtn");
    const aiResponse = document.getElementById("aiResponse");
    const messageInput = document.getElementById("message");

    aiSuggestBtn.addEventListener("click", async () => {
        const brief = messageInput.value.trim();
        if (brief.length < 10) { alert("Please write a short brief first."); return; }

        aiSuggestBtn.disabled = true;
        aiResponse.classList.remove("hidden");
        aiResponse.textContent = "Synthesizing architectural data...";

        try {
            const res = await fetch("https://api.anthropic.com/v1/messages", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                    "x-api-key": ANTHROPIC_API_KEY,
                    "anthropic-version": "2023-06-01",
                    "anthropic-dangerous-direct-browser-access": "true"
                },
                body: JSON.stringify({
                    model: "claude-sonnet-4-20250514",
                    max_tokens: 500,
                    system: "You are the Lead AI Architect for 'PLUG IN'. Given a user's brief, expand it into a 3-point technical roadmap: 1. Agent Logic 2. Interface Layer 3. Neural Sync. Keep it short, futuristic, and professional.",
                    messages: [{ role: "user", content: brief }]
                })
            });
            const data = await res.json();
            const roadmap = data.content?.[0]?.text || "Could not generate roadmap.";
            aiResponse.innerHTML = `<strong style="color:#00f2ff;">PROPOSED ROADMAP:</strong><br>${roadmap.replace(/\n/g, "<br>")}`;
            messageInput.value += "\n\n--- AI ARCHITECT PROPOSAL ---\n" + roadmap;
        } catch (e) {
            aiResponse.textContent = "Connection timed out. Please try again.";
        } finally {
            aiSuggestBtn.disabled = false;
        }
    });

    // ─── ORDER FORM ───────────────────────────────────────────────────────────
    document.getElementById("submitBtn").addEventListener("click", () => {
        const name = document.getElementById("name").value.trim();
        const email = document.getElementById("email").value.trim();
        const type = document.getElementById("type").value;
        const budget = document.getElementById("budget").value;
        const message = document.getElementById("message").value.trim();

        if (!name || !email || !message) { alert("Please fill in all required fields."); return; }

        document.getElementById("successMsg").classList.remove("hidden");
        const subject = encodeURIComponent(`[PLUG IN] ${type} - From ${name}`);
        const body = encodeURIComponent(`System Notification: New Inquiry/Order\n\nName: ${name}\nEmail: ${email}\nType: ${type}\nBudget: ${budget}\n\nBrief:\n${message}`);
        setTimeout(() => {
            window.location.href = `mailto:hello@plugin-agency.ai?subject=${subject}&body=${body}`;
            document.getElementById("name").value = "";
            document.getElementById("email").value = "";
            document.getElementById("message").value = "";
            aiResponse.classList.add("hidden");
            setTimeout(() => document.getElementById("successMsg").classList.add("hidden"), 5000);
        }, 1000);
    });

    // ─── SMOOTH SCROLL ────────────────────────────────────────────────────────
    document.querySelectorAll('a[href^="#"]').forEach(anchor => {
        anchor.addEventListener("click", function(e) {
            e.preventDefault();
            const target = document.querySelector(this.getAttribute("href"));
            if (target) target.scrollIntoView({ behavior: "smooth" });
        });
    });

    // ─── VOICE BTN (stub — wire up your TTS service here) ────────────────────
    document.getElementById("voiceBtn").addEventListener("click", () => {
        const msg = new SpeechSynthesisUtterance("Welcome to PLUG IN. Authentication complete. Your neural agency is ready for initialization.");
        msg.pitch = 0.8;
        msg.rate = 0.9;
        window.speechSynthesis.speak(msg);
    });
    </script>
</body>
    </html>
