<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GitHub Profile Preview</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
            background: linear-gradient(135deg, #0D1117 0%, #161B22 100%);
            color: #c9d1d9;
            padding: 2rem;
            min-height: 100vh;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
        }

        /* Header Section with Walking Animation */
        .header-section {
            text-align: center;
            position: relative;
            padding: 4rem 0;
            background: linear-gradient(135deg, rgba(99, 102, 241, 0.1) 0%, rgba(139, 92, 246, 0.1) 100%);
            border-radius: 20px;
            margin-bottom: 3rem;
            overflow: hidden;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(99, 102, 241, 0.2);
        }

        .animated-walker {
            position: absolute;
            left: -200px;
            bottom: 20px;
            animation: walk 20s linear infinite;
        }

        .walker-svg {
            width: 150px;
            height: 150px;
            filter: drop-shadow(0 0 20px rgba(99, 102, 241, 0.5));
        }

        @keyframes walk {
            0% { left: -200px; }
            100% { left: calc(100% + 200px); }
        }

        .title-wrapper {
            position: relative;
            z-index: 2;
        }

        .main-title {
            font-size: 3.5rem;
            font-weight: 800;
            background: linear-gradient(135deg, #6366f1 0%, #8b5cf6 50%, #ec4899 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 1rem;
            animation: glow 2s ease-in-out infinite alternate;
        }

        @keyframes glow {
            from { filter: drop-shadow(0 0 10px rgba(99, 102, 241, 0.5)); }
            to { filter: drop-shadow(0 0 20px rgba(139, 92, 246, 0.8)); }
        }

        .typing-animation {
            font-size: 1.5rem;
            color: #6366f1;
            font-weight: 600;
            min-height: 2rem;
        }

        /* Rotating Cube Loader */
        .cube-loader-section {
            display: flex;
            justify-content: center;
            margin: 3rem 0;
        }

        .cube-loader {
            position: relative;
            width: 75px;
            height: 75px;
            transform-style: preserve-3d;
            transform: rotateX(-30deg);
            animation: rotateCube 4s linear infinite;
        }

        @keyframes rotateCube {
            0% { transform: rotateX(-30deg) rotateY(0); }
            100% { transform: rotateX(-30deg) rotateY(360deg); }
        }

        .cube-wrapper {
            position: absolute;
            width: 100%;
            height: 100%;
            transform-style: preserve-3d;
        }

        .cube-span {
            position: absolute;
            width: 100%;
            height: 100%;
            background: linear-gradient(to bottom, 
                hsl(330, 3.13%, 25.1%) 0%,
                hsl(176.67, 34.1%, 36.88%) 12.1%,
                hsl(176.66, 53.07%, 46.58%) 36.6%,
                hsl(176.8, 76.78%, 54.08%) 71.7%,
                hsl(176.88, 98.34%, 57.93%) 99%);
        }

        .cube-span:nth-child(1) { transform: rotateY(0deg) translateZ(37.5px); }
        .cube-span:nth-child(2) { transform: rotateY(90deg) translateZ(37.5px); }
        .cube-span:nth-child(3) { transform: rotateY(180deg) translateZ(37.5px); }
        .cube-span:nth-child(4) { transform: rotateY(270deg) translateZ(37.5px); }

        .cube-top {
            position: absolute;
            width: 75px;
            height: 75px;
            background: hsl(330, 3.13%, 25.1%);
            transform: rotateX(90deg) translateZ(37.5px);
        }

        /* Stats Grid */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 2rem;
            margin: 3rem 0;
        }

        .stat-card {
            background: rgba(22, 27, 34, 0.8);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(99, 102, 241, 0.2);
            border-radius: 16px;
            padding: 2rem;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .stat-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(99, 102, 241, 0.1), transparent);
            transition: 0.5s;
        }

        .stat-card:hover::before {
            left: 100%;
        }

        .stat-card:hover {
            transform: translateY(-8px);
            border-color: rgba(99, 102, 241, 0.5);
            box-shadow: 0 20px 40px rgba(99, 102, 241, 0.2);
        }

        .stat-number {
            font-size: 2.5rem;
            font-weight: 800;
            background: linear-gradient(135deg, #6366f1, #8b5cf6);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .stat-label {
            color: #8b949e;
            font-size: 0.9rem;
            margin-top: 0.5rem;
        }

        /* Social Icons with Squircle Clip Path */
        .social-section {
            display: flex;
            justify-content: center;
            gap: 1rem;
            margin: 3rem 0;
            flex-wrap: wrap;
        }

        .social-icon {
            width: 64px;
            height: 64px;
            clip-path: url(#squircleClip);
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            border: 2px solid rgba(255, 255, 255, 0.1);
        }

        .social-icon:hover {
            transform: scale(1.15) translateY(-8px);
            box-shadow: 0 20px 40px rgba(99, 102, 241, 0.4);
        }

        .github-icon { background: linear-gradient(135deg, #333, #666); }
        .linkedin-icon { background: linear-gradient(135deg, #0077B5, #00A0DC); }
        .youtube-icon { background: linear-gradient(135deg, #FF0000, #CC0000); }
        .discord-icon { background: linear-gradient(135deg, #5865F2, #7289DA); }

        .social-icon svg {
            width: 32px;
            height: 32px;
            fill: white;
        }

        /* Code Terminal */
        .code-terminal {
            background: #0D1117;
            border: 1px solid rgba(99, 102, 241, 0.3);
            border-radius: 12px;
            padding: 1.5rem;
            margin: 3rem 0;
            font-family: 'Fira Code', 'Courier New', monospace;
            position: relative;
            overflow: hidden;
        }

        .terminal-header {
            display: flex;
            gap: 0.5rem;
            margin-bottom: 1.5rem;
        }

        .terminal-dot {
            width: 12px;
            height: 12px;
            border-radius: 50%;
        }

        .dot-red { background: #ff5f56; }
        .dot-yellow { background: #ffbd2e; }
        .dot-green { background: #27c93f; }

        .code-line {
            color: #8b949e;
            margin: 0.5rem 0;
            animation: fadeInUp 0.5s ease;
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(10px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .code-keyword { color: #ff7b72; }
        .code-string { color: #a5d6ff; }
        .code-function { color: #d2a8ff; }
        .code-property { color: #7ee787; }

        /* Tech Stack Pills */
        .tech-stack {
            display: flex;
            flex-wrap: wrap;
            gap: 1rem;
            justify-content: center;
            margin: 3rem 0;
        }

        .tech-pill {
            background: linear-gradient(135deg, rgba(99, 102, 241, 0.2), rgba(139, 92, 246, 0.2));
            border: 1px solid rgba(99, 102, 241, 0.4);
            padding: 0.75rem 1.5rem;
            border-radius: 50px;
            font-weight: 600;
            transition: all 0.3s ease;
            cursor: pointer;
        }

        .tech-pill:hover {
            background: linear-gradient(135deg, rgba(99, 102, 241, 0.4), rgba(139, 92, 246, 0.4));
            transform: scale(1.1) rotate(2deg);
            box-shadow: 0 10px 30px rgba(99, 102, 241, 0.3);
        }

        /* Footer Wave */
        .footer {
            margin-top: 5rem;
            text-align: center;
            position: relative;
        }

        .wave-svg {
            width: 100%;
            height: 100px;
        }

        .footer-text {
            font-size: 0.9rem;
            color: #8b949e;
            margin-top: 2rem;
        }

        /* Responsive */
        @media (max-width: 768px) {
            .main-title { font-size: 2rem; }
            .typing-animation { font-size: 1.2rem; }
            .stats-grid { grid-template-columns: 1fr; }
            body { padding: 1rem; }
        }
    </style>
</head>
<body>
    <!-- SVG Definitions -->
    <svg width="0" height="0" style="position: absolute;">
        <defs>
            <clipPath id="squircleClip" clipPathUnits="objectBoundingBox">
                <path d="M 0,0.5 C 0,0 0,0 0.5,0 S 1,0 1,0.5 1,1 0.5,1 0,1 0,0.5"></path>
            </clipPath>
        </defs>
    </svg>

    <div class="container">
        <!-- Header Section -->
        <div class="header-section">
            <div class="animated-walker">
                <svg class="walker-svg" viewBox="0 0 200 200">
                    <circle cx="100" cy="60" r="40" fill="#6366f1"/>
                    <ellipse cx="100" cy="120" rx="30" ry="50" fill="#6366f1"/>
                    <line x1="100" y1="120" x2="80" y2="180" stroke="#6366f1" stroke-width="8" stroke-linecap="round"/>
                    <line x1="100" y1="120" x2="120" y2="180" stroke="#6366f1" stroke-width="8" stroke-linecap="round"/>
                    <line x1="100" y1="100" x2="70" y2="130" stroke="#6366f1" stroke-width="8" stroke-linecap="round"/>
                    <line x1="100" y1="100" x2="130" y2="130" stroke="#6366f1" stroke-width="8" stroke-linecap="round"/>
                </svg>
            </div>
            
            <div class="title-wrapper">
                <h1 class="main-title">👋 Welcome to My Digital Universe</h1>
                <div class="typing-animation" id="typingText"></div>
            </div>
        </div>

        <!-- Cube Loader -->
        <div class="cube-loader-section">
            <div class="cube-loader">
                <div class="cube-top"></div>
                <div class="cube-wrapper">
                    <span class="cube-span"></span>
                    <span class="cube-span"></span>
                    <span class="cube-span"></span>
                    <span class="cube-span"></span>
                </div>
            </div>
        </div>

        <!-- Stats Grid -->
        <div class="stats-grid">
            <div class="stat-card">
                <div class="stat-number">5000+</div>
                <div class="stat-label">Lines of Code Written</div>
            </div>
            <div class="stat-card">
                <div class="stat-number">50+</div>
                <div class="stat-label">Projects Completed</div>
            </div>
            <div class="stat-card">
                <div class="stat-number">20+</div>
                <div class="stat-label">Technologies Mastered</div>
            </div>
            <div class="stat-card">
                <div class="stat-number">∞</div>
                <div class="stat-label">Coffee Cups Consumed</div>
            </div>
        </div>

        <!-- Social Icons -->
        <div class="social-section">
            <div class="social-icon github-icon">
                <svg viewBox="0 0 24 24">
                    <path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/>
                </svg>
            </div>
            <div class="social-icon linkedin-icon">
                <svg viewBox="0 0 24 24">
                    <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
                </svg>
            </div>
            <div class="social-icon youtube-icon">
                <svg viewBox="0 0 24 24">
                    <path d="M23.498 6.186a3.016 3.016 0 0 0-2.122-2.136C19.505 3.545 12 3.545 12 3.545s-7.505 0-9.377.505A3.017 3.017 0 0 0 .502 6.186C0 8.07 0 12 0 12s0 3.93.502 5.814a3.016 3.016 0 0 0 2.122 2.136c1.871.505 9.376.505 9.376.505s7.505 0 9.377-.505a3.015 3.015 0 0 0 2.122-2.136C24 15.93 24 12 24 12s0-3.93-.502-5.814zM9.545 15.568V8.432L15.818 12l-6.273 3.568z"/>
                </svg>
            </div>
            <div class="social-icon discord-icon">
                <svg viewBox="0 0 24 24">
                    <path d="M20.317 4.3698a19.7913 19.7913 0 00-4.8851-1.5152.0741.0741 0 00-.0785.0371c-.211.3753-.4447.8648-.6083 1.2495-1.8447-.2762-3.68-.2762-5.4868 0-.1636-.3933-.4058-.8742-.6177-1.2495a.077.077 0 00-.0785-.037 19.7363 19.7363 0 00-4.8852 1.515.0699.0699 0 00-.0321.0277C.5334 9.0458-.319 13.5799.0992 18.0578a.0824.0824 0 00.0312.0561c2.0528 1.5076 4.0413 2.4228 5.9929 3.0294a.0777.0777 0 00.0842-.0276c.4616-.6304.8731-1.2952 1.226-1.9942a.076.076 0 00-.0416-.1057c-.6528-.2476-1.2743-.5495-1.8722-.8923a.077.077 0 01-.0076-.1277c.1258-.0943.2517-.1923.3718-.2914a.0743.0743 0 01.0776-.0105c3.9278 1.7933 8.18 1.7933 12.0614 0a.0739.0739 0 01.0785.0095c.1202.099.246.1981.3728.2924a.077.077 0 01-.0066.1276 12.2986 12.2986 0 01-1.873.8914.0766.0766 0 00-.0407.1067c.3604.698.7719 1.3628 1.225 1.9932a.076.076 0 00.0842.0286c1.961-.6067 3.9495-1.5219 6.0023-3.0294a.077.077 0 00.0313-.0552c.5004-5.177-.8382-9.6739-3.5485-13.6604a.061.061 0 00-.0312-.0286zM8.02 15.3312c-1.1825 0-2.1569-1.0857-2.1569-2.419 0-1.3332.9555-2.4189 2.157-2.4189 1.2108 0 2.1757 1.0952 2.1568 2.419 0 1.3332-.9555 2.4189-2.1569 2.4189zm7.9748 0c-1.1825 0-2.1569-1.0857-2.1569-2.419 0-1.3332.9554-2.4189 2.1569-2.4189 1.2108 0 2.1757 1.0952 2.1568 2.419 0 1.3332-.9555 2.4189-2.1568 2.4189Z"/>
                </svg>
            </div>
        </div>

        <!-- Code Terminal -->
        <div class="code-terminal">
            <div class="terminal-header">
                <div class="terminal-dot dot-red"></div>
                <div class="terminal-dot dot-yellow"></div>
                <div class="terminal-dot dot-green"></div>
            </div>
            <div class="code-line"><span class="code-keyword">const</span> developer = {</div>
            <div class="code-line">  <span class="code-property">name</span>: <span class="code-string">"Shehan Harsha Kumara"</span>,</div>
            <div class="code-line">  <span class="code-property">role</span>: <span class="code-string">"Full-Stack Developer"</span>,</div>
            <div class="code-line">  <span class="code-property">location</span>: <span class="code-string">"🇱🇰 Sri Lanka"</span>,</div>
            <div class="code-line">  <span class="code-property">passions</span>: [<span class="code-string">"Code"</span>, <span class="code-string">"Gaming"</span>, <span class="code-string">"Innovation"</span>],</div>
            <div class="code-line">  <span class="code-function">build</span>: () => <span class="code-string">"Amazing Things"</span> <span class="code-keyword">🚀</span></div>
            <div class="code-line">};</div>
        </div>

        <!-- Tech Stack -->
        <div class="tech-stack">
            <div class="tech-pill">⚛️ React</div>
            <div class="tech-pill">📱 React Native</div>
            <div class="tech-pill">🎨 Next.js</div>
            <div class="tech-pill">💚 Vue.js</div>
            <div class="tech-pill">🅰️ Angular</div>
            <div class="tech-pill">🔷 TypeScript</div>
            <div class="tech-pill">🟨 JavaScript</div>
            <div class="tech-pill">🐍 Python</div>
            <div class="tech-pill">☕ Java</div>
            <div class="tech-pill">🎯 Dart</div>
            <div class="tech-pill">📦 Node.js</div>
            <div class="tech-pill">🐳 Docker</div>
            <div class="tech-pill">☁️ AWS</div>
            <div class="tech-pill">🔥 Firebase</div>
        </div>

        <!-- Footer -->
        <div class="footer">
            <svg class="wave-svg" viewBox="0 0 1200 100" preserveAspectRatio="none">
                <path d="M0,50 C150,100 350,0 600,50 C850,100 1050,0 1200,50 L1200,100 L0,100 Z" fill="url(#wave-gradient)">
                    <animate attributeName="d" dur="10s" repeatCount="indefinite" 
                        values="M0,50 C150,100 350,0 600,50 C850,100 1050,0 1200,50 L1200,100 L0,100 Z;
                                M0,50 C150,0 350,100 600,50 C850,0 1050,100 1200,50 L1200,100 L0,100 Z;
                                M0,50 C150,100 350,0 600,50 C850,100 1050,0 1200,50 L1200,100 L0,100 Z"/>
                </path>
                <defs>
                    <linearGradient id="wave-gradient" x1="0%" y1="0%" x2="100%" y2="0%">
                        <stop offset="0%" style="stop-color:#6366f1;stop-opacity:0.3"/>
                        <stop offset="50%" style="stop-color:#8b5cf6;stop-opacity:0.3"/>
                        <stop offset="100%" style="stop-color:#ec4899;stop-opacity:0.3"/>
                    </linearGradient>
                </defs>
            </svg>
            <div class="footer-text">
                ⚡ "Code. Game. Repeat." 💀<br>
                Thanks for visiting! Let's build something amazing together 🚀<br>
                <em>⭐️ From shehanharshakumara with 💜</em>
            </div>
        </div>
    </div>

    <script>
        // Typing Animation
        const phrases = [
            "Software Engineering Student 🎓",
            "Full-Stack Developer 💻",
            "UI/UX Enthusiast 🎨",
            "Passionate Gamer 🎮💀",
            "Always Learning New Tech! 🚀"
        ];
        let phraseIndex = 0;
        let charIndex = 0;
        let isDeleting = false;
        const typingElement = document.getElementById('typingText');

        function type() {
            const currentPhrase = phrases[phraseIndex];
            
            if (isDeleting) {
                typingElement.textContent = currentPhrase.substring(0, charIndex - 1);
                charIndex--;
            } else {
                typingElement.textContent = currentPhrase.substring(0, charIndex + 1);
                charIndex++;
            }

            let typingSpeed = isDeleting ? 50 : 100;

            if (!isDeleting && charIndex === currentPhrase.length) {
                typingSpeed = 2000;
                isDeleting = true;
            } else if (isDeleting && charIndex === 0) {
                isDeleting = false;
                phraseIndex = (phraseIndex + 1) % phrases.length;
                typingSpeed = 500;
            }

            setTimeout(type, typingSpeed);
        }

        // Start typing animation
        type();

        // Animate stats on scroll
        const observerOptions = {
            threshold: 0.5
        };

        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.style.animation = 'fadeInUp 0.6s ease';
                }
            });
        }, observerOptions);

        document.querySelectorAll('.stat-card').forEach(card => {
            observer.observe(card);
        });
    </script>
</body>
</html>
