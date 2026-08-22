<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>THIYAGARASAN.exe - Matrix Portfolio</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Courier New', monospace;
            background: #000;
            color: #00FF00;
            overflow-x: hidden;
        }

        .matrix-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: #000;
            overflow: hidden;
            z-index: 0;
        }

        .matrix-char {
            position: absolute;
            color: #00FF00;
            font-family: 'Courier New', monospace;
            font-weight: bold;
            font-size: 1.2rem;
            opacity: 0.15;
            animation: fall linear infinite;
        }

        @keyframes fall {
            0% {
                transform: translateY(-10%);
                opacity: 0;
            }
            10% {
                opacity: 0.3;
            }
            90% {
                opacity: 0.3;
            }
            100% {
                transform: translateY(100vh);
                opacity: 0;
            }
        }

        .matrix-container {
            position: relative;
            z-index: 1;
            padding: 2rem;
            background: rgba(0, 0, 0, 0.85);
            min-height: 100vh;
        }

        .hud-section {
            margin-bottom: 2rem;
            border: 2px solid #00FF00;
            border-radius: 0;
            padding: 1.5rem;
            background: rgba(0, 0, 0, 0.95);
            position: relative;
            overflow: hidden;
        }

        .hud-section::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 2px;
            background: linear-gradient(90deg, transparent, #00FF00, transparent);
            animation: scanline 2s linear infinite;
        }

        @keyframes scanline {
            0% {
                transform: translateY(-2px);
                opacity: 0;
            }
            50% {
                opacity: 1;
            }
            100% {
                transform: translateY(2px);
                opacity: 0;
            }
        }

        .hud-section::after {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 4px;
            height: 100%;
            background: linear-gradient(180deg, #00FF00, transparent);
        }

        .header {
            text-align: center;
            margin-bottom: 3rem;
            position: relative;
            z-index: 2;
        }

        .status-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1.5rem;
            font-size: 0.85rem;
            color: #00FF00;
            font-family: 'Courier New', monospace;
            border: 1px solid #00FF00;
            padding: 0.8rem;
            background: rgba(0, 255, 0, 0.03);
        }

        .status-indicator {
            display: inline-block;
            width: 8px;
            height: 8px;
            background: #00FF00;
            border-radius: 50%;
            margin-right: 0.5rem;
            animation: matrix-pulse 1.5s infinite;
            box-shadow: 0 0 10px #00FF00;
        }

        @keyframes matrix-pulse {
            0%, 100% {
                opacity: 1;
                box-shadow: 0 0 10px #00FF00;
            }
            50% {
                opacity: 0.4;
                box-shadow: 0 0 5px #00FF00;
            }
        }

        .title {
            font-size: 2.5rem;
            margin-bottom: 0.5rem;
            color: #00FF00;
            text-shadow: 0 0 20px #00FF00, 0 0 40px #00FF00;
            letter-spacing: 3px;
            font-family: 'Courier New', monospace;
            font-weight: bold;
            animation: glitch 3s infinite;
        }

        @keyframes glitch {
            0%, 100% {
                text-shadow: 0 0 20px #00FF00, 0 0 40px #00FF00;
            }
            50% {
                text-shadow: 0 0 30px #00FF00, 0 0 60px #00FF00, 0 0 90px #00FF00;
            }
        }

        .subtitle {
            font-size: 0.9rem;
            color: #00FF00;
            letter-spacing: 1px;
            font-family: 'Courier New', monospace;
            animation: flicker 4s infinite;
        }

        @keyframes flicker {
            0%, 100% {
                opacity: 1;
            }
            25% {
                opacity: 0.8;
            }
            50% {
                opacity: 1;
            }
            75% {
                opacity: 0.9;
            }
        }

        .profile-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 2rem;
            margin-bottom: 2rem;
            position: relative;
            z-index: 2;
        }

        .profile-card {
            border: 2px solid #00FF00;
            padding: 1.5rem;
            background: rgba(0, 0, 0, 0.9);
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
        }

        .profile-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(45deg, transparent 30%, rgba(0, 255, 0, 0.1) 50%, transparent 70%);
            animation: shine 3s infinite;
        }

        @keyframes shine {
            0% {
                transform: translateX(-100%);
            }
            100% {
                transform: translateX(100%);
            }
        }

        .profile-card:hover {
            background: rgba(0, 255, 0, 0.1);
            border-color: #00FF00;
            box-shadow: 0 0 20px rgba(0, 255, 0, 0.5), inset 0 0 10px rgba(0, 255, 0, 0.1);
        }

        .profile-card h3 {
            color: #00FF00;
            margin-bottom: 1rem;
            text-transform: uppercase;
            font-size: 0.9rem;
            letter-spacing: 2px;
            font-family: 'Courier New', monospace;
            text-shadow: 0 0 10px #00FF00;
            position: relative;
            z-index: 1;
        }

        .profile-card p {
            color: #00FF00;
            font-size: 0.9rem;
            font-family: 'Courier New', monospace;
            position: relative;
            z-index: 1;
        }

        .tech-stack {
            display: flex;
            flex-wrap: wrap;
            gap: 0.8rem;
            margin-top: 1rem;
            position: relative;
            z-index: 1;
        }

        .tech-badge {
            background: rgba(0, 0, 0, 0.8);
            border: 1px solid #00FF00;
            color: #00FF00;
            padding: 0.4rem 0.8rem;
            font-size: 0.75rem;
            text-transform: uppercase;
            letter-spacing: 1px;
            font-family: 'Courier New', monospace;
            transition: all 0.3s ease;
            cursor: pointer;
        }

        .tech-badge:hover {
            background: #00FF00;
            color: #000;
            box-shadow: 0 0 10px #00FF00;
        }

        .projects-section {
            position: relative;
            z-index: 2;
        }

        .project-item {
            border: 1px solid #00FF00;
            padding: 1.2rem;
            margin-bottom: 1rem;
            background: rgba(0, 0, 0, 0.9);
            transition: all 0.3s ease;
            position: relative;
        }

        .project-item::before {
            content: '► ';
            color: #00FF00;
            animation: blink 1s infinite;
        }

        @keyframes blink {
            0%, 49% {
                opacity: 1;
            }
            50%, 100% {
                opacity: 0;
            }
        }

        .project-item:hover {
            border-color: #00FF00;
            background: rgba(0, 255, 0, 0.05);
            box-shadow: 0 0 15px rgba(0, 255, 0, 0.3);
        }

        .project-name {
            color: #00FF00;
            font-weight: bold;
            margin-bottom: 0.5rem;
            text-transform: uppercase;
            font-size: 0.9rem;
            font-family: 'Courier New', monospace;
            text-shadow: 0 0 10px #00FF00;
        }

        .project-tech {
            color: #00AA00;
            font-size: 0.8rem;
            font-family: 'Courier New', monospace;
        }

        .project-status {
            color: #00FF00;
            font-size: 0.75rem;
            margin-top: 0.5rem;
            letter-spacing: 1px;
            font-family: 'Courier New', monospace;
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 1rem;
            margin-bottom: 2rem;
            position: relative;
            z-index: 2;
        }

        .stat-box {
            border: 2px solid #00FF00;
            padding: 1rem;
            text-align: center;
            background: rgba(0, 0, 0, 0.95);
        }

        .stat-number {
            font-size: 2rem;
            color: #00FF00;
            margin-bottom: 0.5rem;
            font-weight: bold;
            font-family: 'Courier New', monospace;
            text-shadow: 0 0 15px #00FF00;
            animation: pulse-number 2s ease-in-out infinite;
        }

        @keyframes pulse-number {
            0%, 100% {
                transform: scale(1);
            }
            50% {
                transform: scale(1.05);
            }
        }

        .stat-label {
            font-size: 0.75rem;
            color: #00AA00;
            text-transform: uppercase;
            letter-spacing: 1px;
            font-family: 'Courier New', monospace;
        }

        .roadmap {
            position: relative;
            z-index: 2;
        }

        .roadmap-item {
            display: flex;
            align-items: center;
            padding: 0.8rem 0;
            border-bottom: 1px solid rgba(0, 255, 0, 0.2);
            font-size: 0.9rem;
            font-family: 'Courier New', monospace;
        }

        .roadmap-item:last-child {
            border-bottom: none;
        }

        .roadmap-arrow {
            color: #00FF00;
            margin-right: 1rem;
            animation: arrow-move 1.5s ease-in-out infinite;
        }

        @keyframes arrow-move {
            0%, 100% {
                transform: translateX(0);
            }
            50% {
                transform: translateX(5px);
            }
        }

        .roadmap-text {
            color: #00FF00;
        }

        .section-title {
            color: #00FF00;
            text-transform: uppercase;
            letter-spacing: 2px;
            margin-bottom: 1.5rem;
            font-size: 1.1rem;
            font-family: 'Courier New', monospace;
            text-shadow: 0 0 10px #00FF00;
            position: relative;
            z-index: 2;
        }

        .footer {
            text-align: center;
            margin-top: 3rem;
            padding-top: 2rem;
            border-top: 2px solid #00FF00;
            font-size: 0.8rem;
            color: #00FF00;
            position: relative;
            z-index: 2;
            font-family: 'Courier New', monospace;
        }

        .footer a {
            color: #00FF00;
            text-decoration: none;
            transition: all 0.3s ease;
            text-shadow: 0 0 10px #00FF00;
        }

        .footer a:hover {
            color: #ffffff;
            box-shadow: 0 0 20px #00FF00;
        }

        @media (max-width: 768px) {
            .profile-grid {
                grid-template-columns: 1fr;
            }
            .stats-grid {
                grid-template-columns: 1fr;
            }
            .title {
                font-size: 1.8rem;
            }
            .matrix-char {
                font-size: 0.9rem;
            }
        }
    </style>
</head>
<body>
    <div class="matrix-bg" id="matrixBg"></div>

    <div class="matrix-container">
        <div class="status-bar">
            <span><span class="status-indicator"></span>SYSTEM ONLINE</span>
            <span id="time">00:00:00</span>
            <span>v2.0.26 NEURAL_SYNC</span>
        </div>

        <div class="header">
            <div class="title">⚡ THIYAGARASAN.exe ⚡</div>
            <div class="subtitle">>>> FULL-STACK DEVELOPER PROTOCOL ACTIVE</div>
        </div>

        <div class="stats-grid">
            <div class="stat-box">
                <div class="stat-number">7+</div>
                <div class="stat-label">Projects Built</div>
            </div>
            <div class="stat-box">
                <div class="stat-number">10</div>
                <div class="stat-label">Tech Stack</div>
            </div>
            <div class="stat-box">
                <div class="stat-number">2026</div>
                <div class="stat-label">Launch Year</div>
            </div>
        </div>

        <div class="hud-section">
            <div class="profile-grid">
                <div class="profile-card">
                    <h3>🔧 CORE SYSTEMS</h3>
                    <p>Java • C • JavaScript • React • Node.js</p>
                    <div class="tech-stack">
                        <span class="tech-badge">JAVA</span>
                        <span class="tech-badge">C</span>
                        <span class="tech-badge">JS</span>
                        <span class="tech-badge">REACT</span>
                        <span class="tech-badge">NODE.JS</span>
                    </div>
                </div>
                <div class="profile-card">
                    <h3>💾 DATABASE LAYER</h3>
                    <p>MySQL | Git/GitHub | VS Code</p>
                    <div class="tech-stack">
                        <span class="tech-badge">MYSQL</span>
                        <span class="tech-badge">GIT</span>
                        <span class="tech-badge">GITHUB</span>
                    </div>
                </div>
            </div>
        </div>

        <div class="hud-section projects-section">
            <h3 class="section-title">📊 ACTIVE PROJECTS</h3>

            <div class="project-item">
                <div class="project-name">Student Skill Exchange Platform</div>
                <div class="project-tech">JAVA • OOP • MYSQL • MATCHING_ENGINE</div>
                <div class="project-status">⚡ ACTIVE_DEVELOPMENT</div>
            </div>

            <div class="project-item">
                <div class="project-name">React Learning Hub</div>
                <div class="project-tech">REACT • JAVASCRIPT • ES6+</div>
                <div class="project-status">⚡ CONTINUOUS_UPGRADE</div>
            </div>

            <div class="project-item">
                <div class="project-name">DSA Problem Solver</div>
                <div class="project-tech">JAVA • C • ALGORITHM_ANALYSIS</div>
                <div class="project-status">⚡ ONGOING_PRACTICE</div>
            </div>

            <div class="project-item">
                <div class="project-name">Portfolio Website</div>
                <div class="project-tech">HTML • CSS • RESPONSIVE_DESIGN</div>
                <div class="project-status">✓ COMPLETED</div>
            </div>
        </div>

        <div class="hud-section">
            <h3 class="section-title">🚀 2026 ROADMAP</h3>
            <div class="roadmap">
                <div class="roadmap-item">
                    <span class="roadmap-arrow">→</span>
                    <span class="roadmap-text">Master Java + OOP Fundamentals</span>
                </div>
                <div class="roadmap-item">
                    <span class="roadmap-arrow">→</span>
                    <span class="roadmap-text">Advanced React & Component Architecture</span>
                </div>
                <div class="roadmap-item">
                    <span class="roadmap-arrow">→</span>
                    <span class="roadmap-text">Node.js + Express Backend Mastery</span>
                </div>
                <div class="roadmap-item">
                    <span class="roadmap-arrow">→</span>
                    <span class="roadmap-text">Build Full-Stack Applications</span>
                </div>
                <div class="roadmap-item">
                    <span class="roadmap-arrow">→</span>
                    <span class="roadmap-text">Secure Software Development Internship</span>
                </div>
            </div>
        </div>

        <div class="footer">
            <div style="margin-bottom: 1rem;">SIGNAL STRENGTH: ████████░░ | CONNECTIVITY: OPTIMAL</div>
            <div>
                <a href="https://github.com/thiyagarasan6380-alt" target="_blank">[GITHUB]</a>
                <span style="color: #00AA00; margin: 0 0.5rem;">•</span>
                <a href="https://linkedin.com/in/thiyagarasan-c-25bb2b37a" target="_blank">[LINKEDIN]</a>
                <span style="color: #00AA00; margin: 0 0.5rem;">•</span>
                <a href="mailto:thiyagarasan6380@gmail.com">[EMAIL]</a>
            </div>
            <div style="margin-top: 1rem; color: #00FF00;">BUILD • LEARN • SHIP</div>
        </div>
    </div>

    <script>
        // Create Matrix Background with Falling Binary
        function createMatrixChars() {
            const matrixBg = document.getElementById('matrixBg');
            const chars = '01';
            const columns = Math.floor(window.innerWidth / 30);

            // Initial characters
            for (let i = 0; i < columns; i++) {
                createChar(matrixBg, chars);
            }

            // Continuously spawn new characters
            setInterval(() => {
                createChar(matrixBg, chars);
            }, 500);
        }

        function createChar(container, chars) {
            const char = document.createElement('div');
            char.className = 'matrix-char';
            char.textContent = chars[Math.floor(Math.random() * chars.length)];
            char.style.left = Math.random() * 100 + '%';
            char.style.top = -50 + 'px';
            const duration = 10 + Math.random() * 10;
            char.style.animationDuration = duration + 's';
            char.style.animationDelay = Math.random() * 5 + 's';
            container.appendChild(char);

            // Remove character after animation completes
            setTimeout(() => {
                char.remove();
            }, (duration + 5) * 1000);
        }

        // Update Real-time Clock
        function updateTime() {
            const time = new Date();
            const hours = String(time.getHours()).padStart(2, '0');
            const minutes = String(time.getMinutes()).padStart(2, '0');
            const seconds = String(time.getSeconds()).padStart(2, '0');
            document.getElementById('time').textContent = hours + ':' + minutes + ':' + seconds;
        }

        // Initialize
        createMatrixChars();
        updateTime();
        setInterval(updateTime, 1000);

        // Responsive adjustment
        window.addEventListener('resize', () => {
            // Could add responsive logic here if needed
        });
    </script>
</body>
</html>
