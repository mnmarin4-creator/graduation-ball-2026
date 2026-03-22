# graduation-ball-2026
graduation-ball-2026
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GRADUATION BALL 2026 | Star of the Night</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;1,400&family=Montserrat:wght@300;400;600&display=swap" rel="stylesheet">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    <style>
        :root {
            --silver-light: #f1f5f9;
            --silver-metallic: #94a3b8;
            --silver-dark: #475569;
            --black-pure: #020617;
            --black-soft: #0f172a;
        }

        body {
            background-color: var(--black-pure);
            color: var(--silver-light);
            font-family: 'Montserrat', sans-serif;
            overflow-x: hidden;
        }

        h1, h2, h3, .serif-font {
            font-family: 'Playfair Display', serif;
        }

        /* Animated Background */
        .stars {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: -1;
            background: radial-gradient(ellipse at bottom, #1B2735 0%, #090A0F 100%);
        }

        .star {
            position: absolute;
            background: white;
            border-radius: 50%;
            opacity: 0;
            animation: twinkle var(--duration) ease-in-out infinite;
            animation-delay: var(--delay);
        }

        @keyframes twinkle {
            0% { opacity: 0; transform: scale(0.5); }
            50% { opacity: var(--opacity); transform: scale(1); }
            100% { opacity: 0; transform: scale(0.5); }
        }

        /* Glassmorphism */
        .glass-panel {
            background: rgba(255, 255, 255, 0.03);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            box-shadow: 0 4px 30px rgba(0, 0, 0, 0.5);
        }

        .glass-card {
            background: linear-gradient(145deg, rgba(255,255,255,0.05) 0%, rgba(255,255,255,0.01) 100%);
            border: 1px solid rgba(255, 255, 255, 0.1);
            transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        .glass-card:hover {
            transform: translateY(-5px) scale(1.02);
            border-color: rgba(255, 255, 255, 0.3);
            box-shadow: 0 20px 40px rgba(0,0,0,0.4), 0 0 15px rgba(255,255,255,0.1);
        }

        /* Silver Gradient Text */
        .text-silver-gradient {
            background: linear-gradient(to right, #e2e8f0, #94a3b8, #cbd5e1);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-size: 200% auto;
            animation: shine 5s linear infinite;
        }

        @keyframes shine {
            to { background-position: 200% center; }
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #0f172a; 
        }
        ::-webkit-scrollbar-thumb {
            background: #475569; 
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #94a3b8; 
        }

        /* Image Upload Preview */
        .preview-img {
            width: 100%;
            height: 300px;
            object-fit: cover;
            border-radius: 0.5rem;
            filter: grayscale(20%) contrast(1.1);
            transition: filter 0.3s;
        }
        .glass-card:hover .preview-img {
            filter: grayscale(0%) contrast(1.2);
        }

        /* QR Code Container */
        #qrcode img {
            margin: 0 auto;
            border: 5px solid white;
            border-radius: 8px;
        }

        /* Admin Toggle */
        .admin-panel {
            display: none;
        }
        .admin-panel.active {
            display: block;
            animation: fadeIn 0.5s;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .vote-btn {
            background: linear-gradient(45deg, #334155, #1e293b);
            border: 1px solid #94a3b8;
            color: white;
            transition: all 0.3s;
        }
        .vote-btn:hover {
            background: linear-gradient(45deg, #475569, #334155);
            box-shadow: 0 0 15px rgba(148, 163, 184, 0.5);
        }
        .vote-btn.voted {
            background: #059669;
            border-color: #34d399;
            pointer-events: none;
        }
    </style>
</head>
<body class="antialiased min-h-screen flex flex-col">

    <!-- Background Stars -->
    <div class="stars" id="star-container"></div>

    <!-- Header -->
    <header class="w-full py-8 text-center relative z-10 border-b border-white/10 glass-panel">
        <div class="container mx-auto px-4">
            <h2 class="text-sm md:text-base tracking-[0.3em] text-slate-400 uppercase mb-2">Class of 2026 Presents</h2>
            <h1 class="text-5xl md:text-7xl font-bold text-silver-gradient mb-2">GRADUATION BALL</h1>
            <p class="serif-font italic text-xl md:text-2xl text-slate-300">"One Last Dance Before We Shine"</p>
            
            <!-- Live Clock -->
            <div id="clock" class="mt-4 text-slate-500 font-mono text-sm"></div>
        </div>
    </header>

    <!-- Main Content Area -->
    <main class="flex-grow container mx-auto px-4 py-8 relative z-10">
        
        <!-- VIEW: VOTING BOOTH (Public) -->
        <div id="voting-view" class="max-w-6xl mx-auto">
            
            <!-- Category Navigation -->
            <div class="flex flex-wrap justify-center gap-4 mb-12" id="category-tabs">
                <!-- Tabs injected via JS -->
            </div>

            <!-- Nominees Grid -->
            <div id="nominees-grid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
                <!-- Cards injected via JS -->
            </div>

            <!-- Empty State -->
            <div id="empty-state" class="hidden text-center py-20">
                <div class="text-6xl mb-4">✨</div>
                <h3 class="text-2xl text-slate-300">Nominees coming soon...</h3>
                <p class="text-slate-500">The stars are aligning. Check back later!</p>
            </div>
        </div>

        <!-- VIEW: ADMIN DASHBOARD (Hidden by default) -->
        <div id="admin-view" class="admin-panel max-w-4xl mx-auto glass-panel p-8 rounded-xl">
            <div class="flex justify-between items-center mb-8 border-b border-white/10 pb-4">
                <h2 class="text-3xl serif-font text-white">Organizer Dashboard</h2>
                <button onclick="toggleAdmin()" class="text-sm text-red-400 hover:text-red-300">Close Panel</button>
            </div>

            <div class="grid md:grid-cols-2 gap-8">
                <!-- Upload Section -->
                <div class="space-y-6">
                    <h3 class="text-xl text-slate-300 border-l-4 border-slate-500 pl-3">Add Nominee</h3>
                    
                    <div>
                        <label class="block text-sm text-slate-400 mb-1">Category</label>
                        <select id="admin-category" class="w-full bg-slate-800 border border-slate-600 rounded p-2 text-white focus:outline-none focus:border-slate-400">
                            <option value="star-of-the-night">⭐ Star of the Night</option>
                            <option value="darling-of-the-night">💖 Darling of the Night</option>
                            <option value="best-dressed-male">🤵 Best Dressed (Male)</option>
                            <option value="best-dressed-female">👗 Best Dressed (Female)</option>
                            <option value="cutest-couple">💕 Cutest Couple</option>
                        </select>
                    </div>

                    <div>
                        <label class="block text-sm text-slate-400 mb-1">Full Name</label>
                        <input type="text" id="admin-name" class="w-full bg-slate-800 border border-slate-600 rounded p-2 text-white focus:outline-none focus:border-slate-400" placeholder="e.g. Juan Dela Cruz">
                    </div>

                    <div>
                        <label class="block text-sm text-slate-400 mb-1">Photo</label>
                        <div class="relative border-2 border-dashed border-slate-600 rounded-lg p-6 text-center hover:bg-slate-800/50 transition cursor-pointer" onclick="document.getElementById('admin-file').click()">
                            <input type="file" id="admin-file" class="hidden" accept="image/*" onchange="previewFile()">
                            <div id="upload-placeholder" class="text-slate-400">
                                <svg class="mx-auto h-12 w-12 text-slate-500" stroke="currentColor" fill="none" viewBox="0 0 48 48"><path d="M28 8H12a4 4 0 00-4 4v20m32-12v8m0 0v8a4 4 0 01-4 4H12a4 4 0 01-4-4v-4m32-4l-3.172-3.172a4 4 0 00-5.656 0L28 28M8 32l9.172-9.172a4 4 0 015.656 0L28 28m0 0l4 4m4-24h8m-4-4v8m-12 4h.02" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" /></svg>
                                <p class="mt-1 text-xs">Click to upload photo</p>
                            </div>
                            <img id="admin-preview" class="hidden w-full h-48 object-cover rounded mt-2">
                        </div>
                    </div>

                    <button onclick="addNominee()" class="w-full py-3 bg-slate-200 text-slate-900 font-bold rounded hover:bg-white transition shadow-[0_0_15px_rgba(255,255,255,0.3)]">
                        ADD TO BALLOT
                    </button>
                </div>

                <!-- QR & Stats Section -->
                <div class="space-y-6">
                    <h3 class="text-xl text-slate-300 border-l-4 border-slate-500 pl-3">Event Tools</h3>
                    
                    <div class="bg-slate-900/50 p-4 rounded border border-slate-700 text-center">
                        <p class="text-sm text-slate-400 mb-2">Scan to Vote</p>
                        <div id="qrcode" class="bg-white p-2 rounded inline-block"></div>
                        <p class="text-xs text-slate-500 mt-2">Share this link with students</p>
                    </div>

                    <div class="bg-slate-900/50 p-4 rounded border border-slate-700">
                        <h4 class="text-sm font-bold text-slate-300 mb-2">Live Stats</h4>
                        <div id="stats-container" class="space-y-2 text-sm">
                            <!-- Stats injected here -->
                            <div class="text-slate-500 italic">No data yet...</div>
                        </div>
                    </div>

                    <button onclick="clearData()" class="w-full py-2 border border-red-900 text-red-500 rounded hover:bg-red-900/20 transition text-sm">
                        Reset All Data
                    </button>
                </div>
            </div>
        </div>

    </main>

    <!-- Footer -->
    <footer class="w-full py-6 text-center text-slate-600 text-sm relative z-10 border-t border-white/5">
        <p>&copy; 2026 Graduation Committee. All rights reserved.</p>
        <button onclick="promptAdmin()" class="mt-2 text-xs text-slate-700 hover:text-slate-400 transition">Organizer Login</button>
    </footer>

    <!-- Image Modal -->
    <div id="image-modal" class="fixed inset-0 z-50 hidden bg-black/90 backdrop-blur-sm flex items-center justify-center p-4" onclick="closeModal()">
        <img id="modal-img" src="" class="max-h-[90vh] max-w-full rounded shadow-2xl border border-slate-700">
    </div>

    <script>
        // --- DATA STATE ---
        // Structure: { category: [ {id, name, img, votes} ] }
        let appData = {
            "star-of-the-night": [],
            "darling-of-the-night": [],
            "best-dressed-male": [],
            "best-dressed-female": [],
            "cutest-couple": []
        };

        const categoryLabels = {
            "star-of-the-night": "⭐ Star of the Night",
            "darling-of-the-night": "💖 Darling of the Night",
            "best-dressed-male": "🤵 Best Dressed (Male)",
            "best-dressed-female": "👗 Best Dressed (Female)",
            "cutest-couple": "💕 Cutest Couple"
        };

        let currentCategory = "star-of-the-night";
        let votesCast = {}; // Track if user voted per category in this session

        // --- INITIALIZATION ---
        document.addEventListener('DOMContentLoaded', () => {
            createStars();
            startClock();
            renderTabs();
            renderNominees();
            generateQR();
            
            // Load dummy data for demo purposes if empty
            if(localStorage.getItem('gb2026_data')) {
                appData = JSON.parse(localStorage.getItem('gb2026_data'));
                renderNominees();
                updateStats();
            }
        });

        // --- VISUAL EFFECTS ---
        function createStars() {
            const container = document.getElementById('star-container');
            const count = 100;
            for(let i=0; i<count; i++) {
                const star = document.createElement('div');
                star.className = 'star';
                const xy = Math.random() * 100;
                const duration = Math.random() * 3 + 2;
                const size = Math.random() * 2 + 1;
                const delay = Math.random() * 5;
                
                star.style.left = `${Math.random() * 100}%`;
                star.style.top = `${Math.random() * 100}%`;
                star.style.width = `${size}px`;
                star.style.height = `${size}px`;
                star.style.setProperty('--duration', `${duration}s`);
                star.style.setProperty('--delay', `${delay}s`);
                star.style.setProperty('--opacity', Math.random());
                
                container.appendChild(star);
            }
        }

        function startClock() {
            setInterval(() => {
                const now = new Date();
                document.getElementById('clock').innerText = now.toLocaleTimeString();
            }, 1000);
        }

        // --- CORE LOGIC ---

        function renderTabs() {
            const container = document.getElementById('category-tabs');
            container.innerHTML = '';
            
            Object.keys(appData).forEach(key => {
                const btn = document.createElement('button');
                const isActive = key === currentCategory;
                btn.className = `px-6 py-2 rounded-full text-sm font-semibold transition-all duration-300 border ${
                    isActive 
                    ? 'bg-slate-200 text-slate-900 border-slate-200 shadow-[0_0_15px_rgba(255,255,255,0.4)]' 
                    : 'bg-transparent text-slate-400 border-slate-700 hover:border-slate-500 hover:text-slate-200'
                }`;
                btn.innerText = categoryLabels[key];
                btn.onclick = () => {
                    currentCategory = key;
                    renderTabs();
                    renderNominees();
                };
                container.appendChild(btn);
            });
        }

        function renderNominees() {
            const grid = document.getElementById('nominees-grid');
            const empty = document.getElementById('empty-state');
            const nominees = appData[currentCategory];

            grid.innerHTML = '';

            if (nominees.length === 0) {
                grid.classList.add('hidden');
                empty.classList.remove('hidden');
                return;
            }

            grid.classList.remove('hidden');
            empty.classList.add('hidden');

            nominees.forEach((nom, index) => {
                const card = document.createElement('div');
                card.className = 'glass-card rounded-xl overflow-hidden relative group';
                
                // Check if user voted in this category
                const hasVoted = votesCast[currentCategory];
                const isVotedFor = hasVoted === nom.id;
                
                // Vote Button State
                let btnState = '';
                if (hasVoted) {
                    btnState = isVotedFor ? 'voted' : 'opacity-50 cursor-not-allowed';
                }

                card.innerHTML = `
                    <div class="relative overflow-hidden cursor-pointer" onclick="openModal('${nom.img}')">
                        <img src="${nom.img}" class="preview-img" alt="${nom.name}">
                        <div class="absolute inset-0 bg-black/20 group-hover:bg-transparent transition"></div>
                        <div class="absolute bottom-0 left-0 w-full bg-gradient-to-t from-black to-transparent p-4 pt-12">
                            <h3 class="text-xl font-bold text-white serif-font">${nom.name}</h3>
                        </div>
                    </div>
                    <div class="p-4 bg-slate-900/40 flex justify-between items-center border-t border-white/5">
                        <span class="text-xs text-slate-400 uppercase tracking-widest">Contestant #${index + 1}</span>
                        <button onclick="vote('${nom.id}')" id="btn-${nom.id}" class="vote-btn px-4 py-2 rounded text-xs font-bold uppercase tracking-wider ${btnState}">
                            ${isVotedFor ? 'Voted ✓' : 'Vote'}
                        </button>
                    </div>
                `;
                grid.appendChild(card);
            });
        }

        function vote(id) {
            if (votesCast[currentCategory]) {
                alert("You have already voted in this category!");
                return;
            }

            // Record Vote
            const nom = appData[currentCategory].find(n => n.id === id);
            if(nom) {
                nom.votes++;
                votesCast[currentCategory] = id;
                
                // Save to "DB"
                localStorage.setItem('gb2026_data', JSON.stringify(appData));

                // UI Updates
                renderNominees();
                updateStats();
                triggerConfetti();
            }
        }

        function triggerConfetti() {
            const duration = 3000;
            const end = Date.now() + duration;

            (function frame() {
                confetti({
                    particleCount: 5,
                    angle: 60,
                    spread: 55,
                    origin: { x: 0 },
                    colors: ['#ffffff', '#94a3b8', '#cbd5e1']
                });
                confetti({
                    particleCount: 5,
                    angle: 120,
                    spread: 55,
                    origin: { x: 1 },
                    colors: ['#ffffff', '#94a3b8', '#cbd5e1']
                });

                if (Date.now() < end) {
                    requestAnimationFrame(frame);
                }
            }());
        }

        // --- ADMIN FUNCTIONS ---

        function promptAdmin() {
            const pwd = prompt("Enter Organizer Password:");
            if (pwd === "2026") {
                toggleAdmin();
            } else if (pwd) {
                alert("Incorrect Password");
            }
        }

        function toggleAdmin() {
            const view = document.getElementById('admin-view');
            const voting = document.getElementById('voting-view');
            
            if (view.classList.contains('active')) {
                view.classList.remove('active');
                voting.classList.remove('hidden');
            } else {
                view.classList.add('active');
                voting.classList.add('hidden');
                updateStats();
            }
        }

        function previewFile() {
            const file = document.getElementById('admin-file').files[0];
            const preview = document.getElementById('admin-preview');
            const placeholder = document.getElementById('upload-placeholder');

            if (file) {
                const reader = new FileReader();
                reader.onloadend = function() {
                    preview.src = reader.result;
                    preview.classList.remove('hidden');
                    placeholder.classList.add('hidden');
                }
                reader.readAsDataURL(file);
            }
        }

        function addNominee() {
            const cat = document.getElementById('admin-category').value;
            const name = document.getElementById('admin-name').value;
            const fileInput = document.getElementById('admin-file');
            const preview = document.getElementById('admin-preview');

            if (!name || !preview.src || preview.classList.contains('hidden')) {
                alert("Please provide a name and photo.");
                return;
            }

            const newNom = {
                id: Date.now().toString(),
                name: name,
                img: preview.src,
                votes: 0
            };

            appData[cat].push(newNom);
            localStorage.setItem('gb2026_data', JSON.stringify(appData));

            // Reset Form
            document.getElementById('admin-name').value = '';
            fileInput.value = '';
            preview.classList.add('hidden');
            document.getElementById('upload-placeholder').classList.remove('hidden');
            
            // Switch to that category to show result
            currentCategory = cat;
            renderTabs();
            renderNominees();
            updateStats();

            alert("Nominee added successfully!");
        }

        function updateStats() {
            const container = document.getElementById('stats-container');
            container.innerHTML = '';

            Object.keys(appData).forEach(cat => {
                const nominees = appData[cat];
                if (nominees.length > 0) {
                    const totalVotes = nominees.reduce((sum, n) => sum + n.votes, 0);
                    const leader = [...nominees].sort((a,b) => b.votes - a.votes)[0];
                    
                    const div = document.createElement('div');
                    div.className = 'bg-slate-800 p-2 rounded border border-slate-700';
                    div.innerHTML = `
                        <div class="flex justify-between text-slate-300 font-semibold">
                            <span>${categoryLabels[cat]}</span>
                            <span class="text-xs bg-slate-700 px-2 py-1 rounded">${totalVotes} votes</span>
                        </div>
                        ${totalVotes > 0 ? `<div class="text-xs text-green-400 mt-1">🏆 Leading: ${leader.name} (${leader.votes})</div>` : ''}
                    `;
                    container.appendChild(div);
                }
            });
        }

        function clearData() {
            if(confirm("WARNING: This will delete all nominees and votes. Are you sure?")) {
                appData = {
                    "star-of-the-night": [], "darling-of-the-night": [],
                    "best-dressed-male": [], "best-dressed-female": [], "cutest-couple": []
                };
                localStorage.removeItem('gb2026_data');
                renderNominees();
                updateStats();
                alert("Data reset.");
            }
        }

        function generateQR() {
            // Generate QR for current URL
            document.getElementById("qrcode").innerHTML = "";
            new QRCode(document.getElementById("qrcode"), {
                text: window.location.href,
                width: 128,
                height: 128,
                colorDark : "#000000",
                colorLight : "#ffffff",
                correctLevel : QRCode.CorrectLevel.H
            });
        }

        // --- MODAL ---
        function openModal(src) {
            const modal = document.getElementById('image-modal');
            const img = document.getElementById('modal-img');
            img.src = src;
            modal.classList.remove('hidden');
        }

        function closeModal() {
            document.getElementById('image-modal').classList.add('hidden');
        }
    </script>
</body>
</html>
