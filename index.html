<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ultimate Aim Trainer</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body {
            margin: 0;
            overflow: hidden;
            background-color: #0f172a;
            color: white;
            font-family: 'Inter', sans-serif;
            user-select: none;
        }
        canvas {
            display: block;
            cursor: crosshair;
        }
        .ui-panel {
            pointer-events: none;
            position: absolute;
            inset: 0;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            padding: 2rem;
        }
        .interactive {
            pointer-events: auto;
        }
        .glass {
            background: rgba(30, 41, 59, 0.7);
            backdrop-filter: blur(8px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
    </style>
</head>
<body>

    <canvas id="gameCanvas"></canvas>

    <!-- Start Menu -->
    <div id="menu" class="ui-panel items-center justify-center bg-slate-950/80 interactive">
        <div class="glass p-10 rounded-2xl max-w-lg w-full text-center shadow-2xl">
            <h1 class="text-5xl font-black mb-2 italic tracking-tighter text-indigo-400">AIM MASTER</h1>
            <p class="text-slate-400 mb-8">トレーニングモードを選択してください</p>
            
            <div class="grid grid-cols-1 gap-4 mb-8">
                <button onclick="startGame('flick')" class="w-full py-4 bg-indigo-600 hover:bg-indigo-500 rounded-xl font-bold transition transform hover:scale-105">
                    FLICK (瞬発力)
                </button>
                <button onclick="startGame('track')" class="w-full py-4 bg-emerald-600 hover:bg-emerald-500 rounded-xl font-bold transition transform hover:scale-105">
                    TRACKING (追従力)
                </button>
                <button onclick="startGame('precision')" class="w-full py-4 bg-amber-600 hover:bg-amber-500 rounded-xl font-bold transition transform hover:scale-105">
                    PRECISION (正確性)
                </button>
            </div>
            
            <p class="text-xs text-slate-500">Press ESC during game to return menu</p>
        </div>
    </div>

    <!-- HUD -->
    <div id="hud" class="ui-panel hidden">
        <div class="flex justify-between items-start">
            <div class="glass px-6 py-3 rounded-xl">
                <div class="text-xs uppercase text-slate-400">Score</div>
                <div id="scoreDisplay" class="text-3xl font-mono font-bold">0</div>
            </div>
            <div class="text-center">
                <div id="timerDisplay" class="text-5xl font-black text-white drop-shadow-lg">60</div>
                <div id="modeDisplay" class="text-xs uppercase tracking-widest text-indigo-400 mt-1">FLICK MODE</div>
            </div>
            <div class="glass px-6 py-3 rounded-xl text-right">
                <div class="text-xs uppercase text-slate-400">Accuracy</div>
                <div id="accuracyDisplay" class="text-3xl font-mono font-bold">100%</div>
            </div>
        </div>
        
        <div class="flex justify-center">
            <div id="comboContainer" class="text-center opacity-0 transition-opacity">
                <div id="comboCount" class="text-6xl font-black text-indigo-500 italic leading-none">0</div>
                <div class="text-xs font-bold uppercase tracking-widest">Combo</div>
            </div>
        </div>
    </div>

    <!-- Result Screen -->
    <div id="result" class="ui-panel items-center justify-center bg-slate-950/90 hidden interactive">
        <div class="glass p-10 rounded-2xl max-w-md w-full text-center">
            <h2 class="text-3xl font-bold mb-6">Result</h2>
            <div class="space-y-4 mb-8">
                <div class="flex justify-between border-b border-white/10 pb-2">
                    <span class="text-slate-400">Final Score</span>
                    <span id="finalScore" class="font-bold text-xl">0</span>
                </div>
                <div class="flex justify-between border-b border-white/10 pb-2">
                    <span class="text-slate-400">Accuracy</span>
                    <span id="finalAccuracy" class="font-bold text-xl text-emerald-400">0%</span>
                </div>
                <div class="flex justify-between border-b border-white/10 pb-2">
                    <span class="text-slate-400">Avg Response</span>
                    <span id="finalResponse" class="font-bold text-xl">0ms</span>
                </div>
            </div>
            <button onclick="hideResults()" class="w-full py-4 bg-indigo-600 hover:bg-indigo-500 rounded-xl font-bold transition">
                Back to Menu
            </button>
        </div>
    </div>

    <script>
        const canvas = document.getElementById('gameCanvas');
        const ctx = canvas.getContext('2d');
        const menu = document.getElementById('menu');
        const hud = document.getElementById('hud');
        const result = document.getElementById('result');
        
        // Game State
        let gameActive = false;
        let gameMode = 'flick'; // flick, track, precision
        let score = 0;
        let timeLeft = 60;
        let combo = 0;
        let totalClicks = 0;
        let hits = 0;
        let targets = [];
        let lastTargetTime = 0;
        let responseTimes = [];
        let timerInterval;

        function resize() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        }
        window.addEventListener('resize', resize);
        resize();

        class Target {
            constructor(mode) {
                const padding = 100;
                this.x = Math.random() * (canvas.width - padding * 2) + padding;
                this.y = Math.random() * (canvas.height - padding * 2) + padding;
                this.spawnTime = Date.now();
                
                if (mode === 'precision') {
                    this.radius = 10;
                } else if (mode === 'track') {
                    this.radius = 30;
                    this.vx = (Math.random() - 0.5) * 10;
                    this.vy = (Math.random() - 0.5) * 10;
                } else {
                    this.radius = 25;
                }
                
                this.color = mode === 'flick' ? '#6366f1' : (mode === 'track' ? '#10b981' : '#f59e0b');
                this.opacity = 0; // Fade in
            }

            update() {
                if (this.opacity < 1) this.opacity += 0.1;
                
                if (gameMode === 'track') {
                    this.x += this.vx;
                    this.y += this.vy;
                    
                    // Bounce
                    if (this.x - this.radius < 0 || this.x + this.radius > canvas.width) this.vx *= -1;
                    if (this.y - this.radius < 0 || this.y + this.radius > canvas.height) this.vy *= -1;
                }
            }

            draw() {
                ctx.save();
                ctx.globalAlpha = this.opacity;
                
                // Outer Glow
                ctx.shadowBlur = 15;
                ctx.shadowColor = this.color;
                
                // Main Circle
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2);
                ctx.fillStyle = this.color;
                ctx.fill();
                
                // Ring
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.radius + 5, 0, Math.PI * 2);
                ctx.strokeStyle = 'white';
                ctx.lineWidth = 2;
                ctx.stroke();
                
                ctx.restore();
            }

            isHit(mx, my) {
                const dist = Math.sqrt((this.x - mx) ** 2 + (this.y - my) ** 2);
                return dist < this.radius + 5;
            }
        }

        function startGame(mode) {
            gameMode = mode;
            gameActive = true;
            score = 0;
            timeLeft = 30;
            combo = 0;
            totalClicks = 0;
            hits = 0;
            targets = [];
            responseTimes = [];
            
            document.getElementById('modeDisplay').innerText = `${mode.toUpperCase()} MODE`;
            menu.classList.add('hidden');
            hud.classList.remove('hidden');
            result.classList.add('hidden');
            
            spawnTarget();
            
            timerInterval = setInterval(() => {
                timeLeft--;
                document.getElementById('timerDisplay').innerText = timeLeft;
                if (timeLeft <= 0) endGame();
            }, 1000);
            
            animate();
        }

        function spawnTarget() {
            if (gameMode === 'track') {
                if (targets.length === 0) targets.push(new Target(gameMode));
            } else {
                targets = [new Target(gameMode)];
            }
            lastTargetTime = Date.now();
        }

        function endGame() {
            gameActive = false;
            clearInterval(timerInterval);
            hud.classList.add('hidden');
            result.classList.remove('hidden');
            
            const accuracy = totalClicks === 0 ? 0 : Math.round((hits / totalClicks) * 100);
            const avgResponse = responseTimes.length === 0 ? 0 : Math.round(responseTimes.reduce((a,b) => a+b) / responseTimes.length);
            
            document.getElementById('finalScore').innerText = score;
            document.getElementById('finalAccuracy').innerText = accuracy + '%';
            document.getElementById('finalResponse').innerText = avgResponse + 'ms';
        }

        function hideResults() {
            result.classList.add('hidden');
            menu.classList.remove('hidden');
        }

        function animate() {
            if (!gameActive) return;
            
            ctx.fillStyle = '#0f172a';
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            
            targets.forEach(t => {
                t.update();
                t.draw();
            });
            
            // Tracking mode special: continuous hit detection
            if (gameMode === 'track' && isMouseDown) {
                checkHit(lastMousePos.x, lastMousePos.y, true);
            }

            requestAnimationFrame(animate);
        }

        let isMouseDown = false;
        let lastMousePos = { x: 0, y: 0 };

        function checkHit(x, y, isContinuous = false) {
            let hitAny = false;
            
            for (let i = 0; i < targets.length; i++) {
                if (targets[i].isHit(x, y)) {
                    hitAny = true;
                    if (gameMode !== 'track') {
                        const reaction = Date.now() - lastTargetTime;
                        responseTimes.push(reaction);
                        targets.splice(i, 1);
                        spawnTarget();
                    }
                    break;
                }
            }

            if (hitAny) {
                hits++;
                combo++;
                score += 10 * (1 + Math.floor(combo / 5));
                updateHUD();
                showCombo();
            } else if (!isContinuous) {
                combo = 0;
                hideCombo();
            }
            
            if (!isContinuous) totalClicks++;
            updateHUD();
        }

        function updateHUD() {
            document.getElementById('scoreDisplay').innerText = score;
            const acc = totalClicks === 0 ? 100 : Math.round((hits / totalClicks) * 100);
            document.getElementById('accuracyDisplay').innerText = acc + '%';
        }

        function showCombo() {
            const el = document.getElementById('comboContainer');
            const count = document.getElementById('comboCount');
            if (combo > 1) {
                el.style.opacity = '1';
                count.innerText = combo;
                count.style.transform = 'scale(1.2)';
                setTimeout(() => count.style.transform = 'scale(1)', 100);
            }
        }

        function hideCombo() {
            document.getElementById('comboContainer').style.opacity = '0';
        }

        // Input Listeners
        window.addEventListener('mousedown', (e) => {
            if (!gameActive) return;
            isMouseDown = true;
            lastMousePos = { x: e.clientX, y: e.clientY };
            checkHit(e.clientX, e.clientY);
        });

        window.addEventListener('mouseup', () => isMouseDown = false);
        window.addEventListener('mousemove', (e) => {
            lastMousePos = { x: e.clientX, y: e.clientY };
        });

        window.addEventListener('keydown', (e) => {
            if (e.key === 'Escape') endGame();
        });
    </script>
</body>
</html>
