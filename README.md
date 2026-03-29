<html lang="mn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Хүндэт гишүүдээ! ❤💐</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Comfortaa:wght@400;700&family=Montserrat:wght@300;600&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Montserrat', sans-serif;
            background: radial-gradient(circle at center, #1e1b4b 0%, #020617 100%);
            margin: 0;
            height: 100vh;
            overflow: hidden;
            color: white;
        }
        @keyframes twinkle {
            0%, 100% { opacity: 0.3; transform: scale(1); }
            50% { opacity: 1; transform: scale(1.1); }
        }
        @keyframes float {
            0%, 100% { transform: translateY(0px) rotate(0deg); }
            50% { transform: translateY(-15px) rotate(2deg); }
        }
        .animate-float { animation: float 4s ease-in-out infinite; }
        .image-glow {
            filter: drop-shadow(0 0 20px rgba(255, 255, 255, 0.4));
            transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }
        .image-glow:hover {
            filter: drop-shadow(0 0 35px rgba(255, 255, 255, 0.7));
            transform: scale(1.08);
        }
        .paper-texture {
            background-color: #fffaf0;
            background-image: radial-gradient(#ede1cc 1px, transparent 0);
            background-size: 24px 24px;
        }
        .handwritten { font-family: 'Comfortaa', cursive; }
        @keyframes bloomUp {
            0% { transform: translateY(100px) scale(0); opacity: 0; }
            60% { opacity: 1; }
            100% { transform: translateY(-20px) scale(1.4); opacity: 1; }
        }
        .flower-bloom {
            position: absolute;
            bottom: -20px;
            animation: bloomUp 2s cubic-bezier(0.22, 1, 0.36, 1) forwards;
        }
    </style>
</head>
<body class="flex flex-col items-center justify-center relative selection:bg-rose-400">
    <audio id="bgMusic" loop>
        <source src="music.mp3" type="audio/mpeg">
    </audio>
    <div id="stars-container" class="absolute inset-0 pointer-events-none z-0"></div>
    <div id="initialScene" class="relative z-10 flex flex-col items-center text-center px-6 transition-all duration-1000">
        <div class="mb-8 animate-float">
            <div class="relative group">
                <img id="mainImage" src="ssssss.jpg" alt="Bird" 
                     onerror="this.style.display='none'; document.getElementById('alt-icon').style.display='block';"
                     class="w-48 h-48 md:w-60 md:h-60 object-contain cursor-pointer image-glow select-none rounded-3xl shadow-2xl">
                <div id="alt-icon" class="hidden text-9xl cursor-pointer animate-bounce">🐦</div>
            </div>
        </div>
        <h2 class="text-rose-100 text-xl md:text-2xl tracking-[0.3em] font-light uppercase animate-pulse">
            Зураг дээр дараарай хөөрхөнөө ✨
        </h2>
    </div>
    <div id="letterScene" class="fixed inset-0 bg-black/90 backdrop-blur-xl z-40 hidden flex items-center justify-center p-4 opacity-0 transition-opacity duration-700">
        <div id="letterBox" class="paper-texture max-w-md w-full rounded-3xl shadow-2xl p-8 md:p-10 transform scale-90 transition-all duration-700 relative border-b-8 border-rose-200">
            <div class="absolute top-0 left-0 w-full h-2 bg-gradient-to-r from-rose-400 via-rose-500 to-rose-400"></div>
            <div class="text-center mb-6"><span class="text-5xl inline-block animate-bounce">💌</span></div>
            <div class="handwritten text-slate-800 space-y-4">
                <h1 class="text-2xl md:text-3xl font-bold text-rose-600 leading-tight">Клубийн уулзалтаа мартаагүй биз дээ!</h1>
                <p class="text-lg md:text-xl leading-relaxed">
                    Сайн уу? Бид 03-р сарын 31-ний 17:30-д <span class="bg-rose-100 px-1 rounded font-bold text-rose-700 text-nowrap">МУИС-ийн 2-р байрны 446 тоотод</span> таныг хүлээж байх болно.
                </p>
                <p class="text-rose-500 font-semibold italic text-right">— Хоцролгүй ирээрэй манайхаан!</p>
                <div class="pt-6 border-t border-slate-200"><p class="text-center text-slate-500 italic">Ирнэ биз дээ? 🥺</p></div>
            </div>
            <div class="mt-8 flex justify-center gap-4 h-16 items-center" id="btnContainer">
                <button id="yesBtn" class="bg-rose-500 hover:bg-rose-600 text-white px-8 py-3 rounded-full text-lg font-bold shadow-lg transition-all active:scale-90">Тийм ээ ✅</button>
                <button id="noBtn" class="bg-slate-300 text-slate-600 px-8 py-3 rounded-full text-lg font-bold transition-all duration-200">Үгүй ❌</button>
            </div>
        </div>
    </div>
    <div id="garden" class="absolute bottom-0 w-full h-32 pointer-events-none flex items-end justify-center z-20"></div>
    <script>
        const audio = document.getElementById('bgMusic');
        const mainImg = document.getElementById('mainImage');
        const altIcon = document.getElementById('alt-icon');
        const initialScene = document.getElementById('initialScene');
        const letterScene = document.getElementById('letterScene');
        const letterBox = document.getElementById('letterBox');
        const yesBtn = document.getElementById('yesBtn');
        const noBtn = document.getElementById('noBtn');
        // Одууд үүсгэх хэсэг (хэвээрээ)
        const starsContainer = document.getElementById('stars-container');
        for (let i = 0; i < 150; i++) {
            const star = document.createElement('div');
            star.style.position = 'absolute';
            star.style.width = Math.random() * 3 + 'px';
            star.style.height = star.style.width;
            star.style.backgroundColor = 'white';
            star.style.borderRadius = '50%';
            star.style.top = Math.random() * 100 + '%';
            star.style.left = Math.random() * 100 + '%';
            star.style.animation = `twinkle ${Math.random() * 3 + 2}s infinite ease-in-out`;
            starsContainer.appendChild(star);
        }
        // --- ДУУ ЭХЛҮҮЛЭХ БА ЗАХИА НЭЭХ ---
        const openLetter = () => {
            // Дууг тоглуулж эхлэх
            audio.play().catch(error => console.log("Дуу тоглуулахад алдаа гарлаа:", error));
            initialScene.style.opacity = '0';
            initialScene.style.transform = 'translateY(-20px)';
            setTimeout(() => {
                initialScene.classList.add('hidden');
                letterScene.classList.remove('hidden');
                setTimeout(() => {
                    letterScene.classList.add('opacity-100');
                    letterBox.classList.remove('scale-90');
                }, 50);
            }, 500);
        };
        mainImg.addEventListener('click', openLetter);
        altIcon.addEventListener('click', openLetter);
        // "Үгүй" товч зугтах
        noBtn.addEventListener('mouseover', () => {
            const container = letterBox.getBoundingClientRect();
            const newX = Math.random() * (container.width - 120) - (container.width / 2) + 60;
            const newY = Math.random() * (container.height - 150) - (container.height / 3);
            noBtn.style.transform = `translate(${newX}px, ${newY}px)`;
        });
        // "Тийм" товч
        yesBtn.addEventListener('click', () => {
            letterBox.style.transform = 'scale(0) rotate(15deg)';
            letterScene.style.opacity = '0';
            setTimeout(() => {
                letterScene.classList.add('hidden');
                startFinale();
            }, 600);
        });
        function startFinale() {
            const emojis = ['🌹', '🌸', '✨', '💖', '🌼', '🌷', '🦋', '🎈'];
            for (let i = 0; i < 70; i++) {
                setTimeout(() => {
                    const f = document.createElement('div');
                    f.className = 'flower-bloom text-4xl md:text-5xl';
                    f.style.left = Math.random() * 100 + '%';
                    f.innerText = emojis[Math.floor(Math.random() * emojis.length)];
                    document.getElementById('garden').appendChild(f);
                }, i * 60);
            }
            setTimeout(() => {
                const finish = document.createElement('div');
                finish.className = 'fixed inset-0 flex flex-col items-center justify-center text-center px-6 z-50 animate-pulse';
                finish.innerHTML = `
                    <h1 class="handwritten text-5xl md:text-7xl font-bold text-white drop-shadow-lg mb-4">Баярлалаа! ❤️</h1>
                    <p class="text-xl md:text-2xl text-rose-200 font-light tracking-widest uppercase">Уулзалтандаа заавал ирээрэй ✨</p>
                `;
                document.body.appendChild(finish);
            }, 2000);
        }
    </script>
</body>
</html>
