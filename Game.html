```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Mexikanisches Wüsten-Rennen</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap');
        
        body {
            background-color: #fcd34d; /* Warmes Wüstengelb */
            font-family: 'Press Start 2P', cursive;
            touch-action: none; /* Verhindert Scrollen beim Spielen auf Mobile */
            overflow: hidden;
        }

        #gameCanvas {
            image-rendering: pixelated;
            box-shadow: 0 10px 25px rgba(0,0,0,0.2);
            background: linear-gradient(to bottom, #fb923c 0%, #fef08a 100%);
        }

        /* Verhindert Textmarkierung bei den Buttons */
        .no-select {
            user-select: none;
            -webkit-user-select: none;
        }
    </style>
</head>
<body class="h-screen w-screen flex flex-col items-center justify-center p-2">

    <!-- Header / Score -->
    <div class="w-full max-w-3xl flex justify-between items-center mb-2 px-4">
        <div class="text-orange-900 text-xs md:text-sm">
            Punkte: <span id="scoreEl">0</span>
        </div>
        <div class="text-orange-900 text-xs md:text-sm">
            Highscore: <span id="highScoreEl">0</span>
        </div>
    </div>

    <!-- Game Container -->
    <div class="relative w-full max-w-3xl aspect-[2/1]">
        <canvas id="gameCanvas" width="800" height="400" class="w-full h-full rounded-lg"></canvas>
        
        <!-- Start / Game Over Overlay -->
        <div id="uiScreen" class="absolute inset-0 flex flex-col items-center justify-center bg-black/60 rounded-lg text-white text-center">
            <h1 id="titleText" class="text-xl md:text-3xl text-yellow-400 mb-4 leading-relaxed">¡Wüsten Rennen!</h1>
            <p id="subText" class="text-xs md:text-sm mb-6 text-gray-200">Drücke Leertaste oder tippe hier</p>
            <button id="startBtn" class="bg-orange-500 hover:bg-orange-600 text-white font-bold py-3 px-6 border-b-4 border-orange-700 hover:border-orange-500 rounded text-xs md:text-sm transition-all active:scale-95 no-select">
                SPIEL STARTEN
            </button>
        </div>
    </div>

    <!-- Mobile Controls (nur sichtbar auf kleinen Bildschirmen oder wenn Touch genutzt wird) -->
    <div class="w-full max-w-3xl flex justify-between mt-6 px-4 gap-4 md:hidden">
        <button id="btnDuck" class="flex-1 bg-red-500 active:bg-red-600 text-white py-6 rounded-xl border-b-8 border-red-700 active:border-b-0 active:translate-y-2 transition-all text-xs font-bold no-select">
            👇 DUCKEN
        </button>
        <button id="btnJump" class="flex-1 bg-green-500 active:bg-green-600 text-white py-6 rounded-xl border-b-8 border-green-700 active:border-b-0 active:translate-y-2 transition-all text-xs font-bold no-select">
            SPRINGEN 👆
        </button>
    </div>

    <div class="mt-4 text-[10px] text-orange-800 text-center md:block hidden opacity-70">
        Steuerung: [Pfeil AUF] oder [Leertaste] = Springen | [Pfeil AB] = Ducken
    </div>

    <script>
        const canvas = document.getElementById('gameCanvas');
        const ctx = canvas.getContext('2d');
        
        const uiScreen = document.getElementById('uiScreen');
        const startBtn = document.getElementById('startBtn');
        const titleText = document.getElementById('titleText');
        const scoreEl = document.getElementById('scoreEl');
        const highScoreEl = document.getElementById('highScoreEl');
        
        const btnDuck = document.getElementById('btnDuck');
        const btnJump = document.getElementById('btnJump');

        // Spielvariablen
        let frames = 0;
        let gameSpeed = 5;
        let score = 0;
        let highScore = localStorage.getItem('mexicanRunHighScore') || 0;
        highScoreEl.innerText = highScore;
        let isGameActive = false;
        let reqAnimation;

        // Konstanten
        const GROUND_Y = 340;

        // Wüsten-Boden Dekor (Berge/Kakteen im Hintergrund)
        const bgElements = [];

        // Spieler-Objekt
        const player = {
            x: 50,
            y: 0,
            width: 40,
            height: 80,
            normalHeight: 80,
            duckHeight: 40,
            dy: 0,
            jumpForce: -13,
            gravity: 0.7,
            grounded: false,
            isDucking: false,

            draw() {
                // Hitbox für Debugging
                // ctx.fillStyle = 'rgba(255, 0, 0, 0.5)';
                // ctx.fillRect(this.x, this.y, this.width, this.height);

                ctx.save();
                ctx.translate(this.x + this.width / 2, this.y + this.height);

                if (this.isDucking) {
                    // Spieler duckt sich
                    ctx.font = "40px Arial";
                    ctx.textAlign = "center";
                    ctx.fillText("😴", 0, -5);
                    // Sombrero tiefer
                    ctx.font = "45px Arial";
                    ctx.fillText("🤠", 0, -35);
                } else {
                    // Spieler normal
                    ctx.font = "60px Arial";
                    ctx.textAlign = "center";
                    ctx.fillText("🏃🏽", 0, -5);
                    // Sombrero
                    ctx.font = "50px Arial";
                    ctx.fillText("🤠", 0, -55);
                }
                ctx.restore();
            },

            update() {
                // Schwerkraft
                this.dy += this.gravity;
                this.y += this.dy;

                // Bodenkollision
                if (this.y + this.height >= GROUND_Y) {
                    this.y = GROUND_Y - this.height;
                    this.dy = 0;
                    this.grounded = true;
                } else {
                    this.grounded = false;
                }
            },

            jump() {
                if (this.grounded && !this.isDucking) {
                    this.dy = this.jumpForce;
                    this.grounded = false;
                }
            },

            duck() {
                if (!this.isDucking && this.grounded) {
                    this.isDucking = true;
                    this.height = this.duckHeight;
                    this.y = GROUND_Y - this.height; // Direkt auf Boden setzen
                }
            },

            standUp() {
                if (this.isDucking) {
                    this.isDucking = false;
                    this.height = this.normalHeight;
                    this.y = GROUND_Y - this.height;
                }
            }
        };

        // Hindernisse
        let obstacles = [];

        class Obstacle {
            constructor(type) {
                this.type = type; // 'ground' (Kaktus) oder 'air' (Piñata)
                this.x = canvas.width;
                
                if (this.type === 'ground') {
                    this.width = 40;
                    this.height = 60 + Math.random() * 20; // Variierende Kaktusgröße
                    this.y = GROUND_Y - this.height;
                } else {
                    // Fliegendes Hindernis
                    this.width = 50;
                    this.height = 50;
                    this.y = GROUND_Y - player.normalHeight - 20; // Ziemlich genau auf Kopfhöhe
                }
            }

            draw() {
                // Hitbox für Debugging
                // ctx.fillStyle = 'rgba(0, 0, 255, 0.5)';
                // ctx.fillRect(this.x, this.y, this.width, this.height);

                ctx.save();
                ctx.translate(this.x + this.width / 2, this.y + this.height);
                
                ctx.textAlign = "center";
                if (this.type === 'ground') {
                    ctx.font = "60px Arial";
                    ctx.fillText("🌵", 0, 5);
                } else {
                    ctx.font = "50px Arial";
                    // Kleine Animation für die Piñata
                    const swing = Math.sin(frames * 0.1) * 5;
                    ctx.fillText("🪅", 0, -5 + swing);
                    
                    // Seil nach oben zeichnen
                    ctx.beginPath();
                    ctx.moveTo(0, -45 + swing);
                    ctx.lineTo(0, -200);
                    ctx.strokeStyle = "#451a03";
                    ctx.lineWidth = 2;
                    ctx.stroke();
                }
                ctx.restore();
            }

            update() {
                this.x -= gameSpeed;
            }
        }

        function initBackground() {
            bgElements.length = 0;
            for(let i=0; i<5; i++) {
                bgElements.push({
                    x: Math.random() * canvas.width,
                    y: GROUND_Y - (20 + Math.random() * 50),
                    size: 30 + Math.random() * 40,
                    speed: 0.5 + Math.random() * 1
                });
            }
        }

        function drawBackground() {
            // Sonne
            ctx.fillStyle = "#facc15";
            ctx.beginPath();
            ctx.arc(100, 100, 40, 0, Math.PI * 2);
            ctx.fill();

            // Wolken/Berge
            bgElements.forEach(bg => {
                ctx.fillStyle = "#d97706"; // Dunkleres Orange für Berge
                ctx.beginPath();
                ctx.moveTo(bg.x, GROUND_Y);
                ctx.lineTo(bg.x + bg.size, bg.y);
                ctx.lineTo(bg.x + bg.size * 2, GROUND_Y);
                ctx.fill();

                // Parallax Scrolling
                if (isGameActive) bg.x -= bg.speed * (gameSpeed * 0.2);
                
                if (bg.x + bg.size * 2 < 0) {
                    bg.x = canvas.width;
                    bg.y = GROUND_Y - (20 + Math.random() * 50);
                }
            });

            // Boden
            ctx.fillStyle = "#b45309";
            ctx.fillRect(0, GROUND_Y, canvas.width, canvas.height - GROUND_Y);
            
            // Sand details
            ctx.fillStyle = "#92400e";
            ctx.fillRect(0, GROUND_Y, canvas.width, 10);
        }

        function handleObstacles() {
            // Spawning
            let spawnRate = Math.max(60, 120 - Math.floor(gameSpeed * 5)); // Wird schneller gespawnt, wenn Speed steigt
            
            if (frames % spawnRate === 0) {
                // 30% Chance auf fliegendes Hindernis
                let type = Math.random() < 0.3 ? 'air' : 'ground';
                obstacles.push(new Obstacle(type));
            }

            for (let i = 0; i < obstacles.length; i++) {
                let obs = obstacles[i];
                obs.update();
                obs.draw();

                // Kollisionserkennung (AABB)
                // Wir machen die Hitboxen etwas toleranter (kleiner), damit es sich fairer anfühlt
                let tolerance = 10;
                
                if (
                    player.x + tolerance < obs.x + obs.width - tolerance &&
                    player.x + player.width - tolerance > obs.x + tolerance &&
                    player.y + tolerance < obs.y + obs.height - tolerance &&
                    player.y + player.height - tolerance > obs.y + tolerance
                ) {
                    gameOver();
                }

                // Entfernen wenn aus dem Bild
                if (obs.x + obs.width < 0) {
                    obstacles.splice(i, 1);
                    i--;
                    score += 10;
                    scoreEl.innerText = score;
                    
                    // Spiel graduell schneller machen
                    if (score % 50 === 0) {
                        gameSpeed += 0.5;
                    }
                }
            }
        }

        function gameLoop() {
            if (!isGameActive) return;

            ctx.clearRect(0, 0, canvas.width, canvas.height);
            
            drawBackground();
            
            player.update();
            player.draw();
            
            handleObstacles();

            frames++;
            reqAnimation = requestAnimationFrame(gameLoop);
        }

        function startGame() {
            player.y = GROUND_Y - player.normalHeight;
            player.dy = 0;
            player.standUp();
            obstacles = [];
            score = 0;
            scoreEl.innerText = score;
            gameSpeed = 6;
            frames = 0;
            isGameActive = true;
            uiScreen.classList.add('hidden');
            
            initBackground();
            cancelAnimationFrame(reqAnimation);
            gameLoop();
        }

        function gameOver() {
            isGameActive = false;
            titleText.innerText = "¡Ay Caramba!";
            subText.innerText = "Du hast die Kakteen geküsst.";
            startBtn.innerText = "NOCHMAL VERSUCHEN";
            uiScreen.classList.remove('hidden');

            if (score > highScore) {
                highScore = score;
                localStorage.setItem('mexicanRunHighScore', highScore);
                highScoreEl.innerText = highScore;
            }
        }

        // --- Steuerung Event-Listener ---

        // Tastatur
        window.addEventListener('keydown', (e) => {
            if ((e.code === 'Space' || e.code === 'ArrowUp' || e.code === 'KeyW') && !e.repeat) {
                if (isGameActive) player.jump();
                else startGame();
            }
            if ((e.code === 'ArrowDown' || e.code === 'KeyS') && !e.repeat) {
                if (isGameActive) player.duck();
            }
        });

        window.addEventListener('keyup', (e) => {
            if (e.code === 'ArrowDown' || e.code === 'KeyS') {
                if (isGameActive) player.standUp();
            }
        });

        // Touch / Buttons (Mobile)
        startBtn.addEventListener('click', startGame);
        uiScreen.addEventListener('click', (e) => {
            if(e.target === uiScreen) startGame();
        });

        // Jump Button
        btnJump.addEventListener('touchstart', (e) => { e.preventDefault(); if (isGameActive) player.jump(); });
        btnJump.addEventListener('mousedown', (e) => { e.preventDefault(); if (isGameActive) player.jump(); });

        // Duck Button
        btnDuck.addEventListener('touchstart', (e) => { e.preventDefault(); if (isGameActive) player.duck(); });
        btnDuck.addEventListener('mousedown', (e) => { e.preventDefault(); if (isGameActive) player.duck(); });
        
        btnDuck.addEventListener('touchend', (e) => { e.preventDefault(); if (isGameActive) player.standUp(); });
        btnDuck.addEventListener('mouseup', (e) => { e.preventDefault(); if (isGameActive) player.standUp(); });
        btnDuck.addEventListener('mouseleave', (e) => { e.preventDefault(); if (isGameActive) player.standUp(); });

        // Initiales Zeichnen
        initBackground();
        drawBackground();
        player.y = GROUND_Y - player.height;
        player.draw();

    </script>
</body>
</html>

```
