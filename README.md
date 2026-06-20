<!DOCTYPE html>
<html lang="si">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GTK - Ultra Premium Music Hub with Gemini AI</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts (Space Grotesk, Syne, Noto Sans Sinhala) -->
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+Sinhala:wght@300;500;700;900&family=Space+Grotesk:wght@300;500;700&family=Syne:wght@700;800&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --glow-color: #00f3ff;
            --accent-pink: #ff007f;
            --primary-purple: #7000ff;
        }

        body {
            font-family: 'Space Grotesk', 'Noto Sans Sinhala', sans-serif;
            background: #03000a;
            overflow-x: hidden;
            position: relative;
        }

        /* පසුබිම් සජීවී ආලෝක තරංග */
        .ambient-glow-1 {
            position: absolute;
            top: -10%;
            left: -10%;
            width: 60vw;
            height: 60vw;
            background: radial-gradient(circle, rgba(112, 0, 255, 0.15) 0%, rgba(0, 0, 0, 0) 70%);
            border-radius: 50%;
            z-index: -1;
            animation: floatGlow 12s infinite alternate ease-in-out;
        }

        .ambient-glow-2 {
            position: absolute;
            bottom: -10%;
            right: -10%;
            width: 50vw;
            height: 50vw;
            background: radial-gradient(circle, rgba(255, 0, 127, 0.12) 0%, rgba(0, 0, 0, 0) 70%);
            border-radius: 50%;
            z-index: -1;
            animation: floatGlow 15s infinite alternate-reverse ease-in-out;
        }

        @keyframes floatGlow {
            0% { transform: translate(0, 0) scale(1); }
            100% { transform: translate(50px, 50px) scale(1.1); }
        }

        /* Glassmorphism Panel effects */
        .glass-card {
            background: rgba(10, 8, 20, 0.55);
            backdrop-filter: blur(25px);
            -webkit-backdrop-filter: blur(25px);
            border: 1px solid rgba(255, 255, 255, 0.08);
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.5);
        }

        .glass-card:hover {
            border-color: rgba(255, 255, 255, 0.15);
            box-shadow: 0 20px 50px rgba(112, 0, 255, 0.15);
        }

        .syne-font {
            font-family: 'Syne', sans-serif;
        }

        /* Glowing texts */
        .neon-glow-cyan {
            text-shadow: 0 0 15px rgba(0, 243, 255, 0.6), 0 0 30px rgba(0, 243, 255, 0.2);
        }

        .neon-glow-pink {
            text-shadow: 0 0 15px rgba(255, 0, 127, 0.6), 0 0 30px rgba(255, 0, 127, 0.2);
        }

        /* vinyl cover animation */
        .spin-music {
            animation: spinDisc 20s linear infinite;
        }

        .spin-paused {
            animation-play-state: paused;
        }

        @keyframes spinDisc {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        input[type="range"] {
            -webkit-appearance: none;
            appearance: none;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 9999px;
            height: 6px;
        }

        input[type="range"]::-webkit-slider-thumb {
            -webkit-appearance: none;
            height: 14px;
            width: 14px;
            border-radius: 50%;
            background: #00f3ff;
            box-shadow: 0 0 10px #00f3ff, 0 0 20px #00f3ff;
            cursor: pointer;
            transition: transform 0.1s;
        }

        input[type="range"]::-webkit-slider-thumb:hover {
            transform: scale(1.3);
        }

        .button-glow:hover {
            box-shadow: 0 0 20px rgba(0, 243, 255, 0.4);
            transform: translateY(-2px);
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 5px;
        }
        ::-webkit-scrollbar-track {
            background: rgba(255, 255, 255, 0.01);
        }
        ::-webkit-scrollbar-thumb {
            background: rgba(255, 255, 255, 0.1);
            border-radius: 10px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #00f3ff;
        }
    </style>
</head>
<body class="text-gray-100 min-h-screen flex flex-col justify-between">

    <!-- සජීවී පසුබිම් Glows -->
    <div class="ambient-glow-1"></div>
    <div class="ambient-glow-2"></div>

    <!-- Header (ශීර්ෂකය) -->
    <header class="w-full py-5 px-6 md:px-12 glass-card flex justify-between items-center z-10 border-b border-white/5">
        <div class="flex items-center space-x-4">
            <div class="relative flex items-center justify-center">
                <div class="absolute inset-0 bg-cyan-400 rounded-full blur-lg opacity-40 animate-pulse"></div>
                <div class="relative bg-gradient-to-tr from-cyan-400 to-fuchsia-600 p-3 rounded-2xl shadow-xl">
                    <i class="fa-solid fa-compact-disc text-2xl text-white spin-music" id="logo-disc"></i>
                </div>
            </div>
            <div>
                <h1 class="text-3xl font-black tracking-widest syne-font bg-gradient-to-r from-cyan-400 via-pink-500 to-purple-500 bg-clip-text text-transparent">GTK</h1>
                <span class="text-[9px] tracking-[0.25em] text-cyan-400 font-bold block -mt-1">INTELLIGENT MUSIC SUITE</span>
            </div>
        </div>
        
        <div class="flex items-center space-x-6">
            <div class="hidden md:flex items-center space-x-4 text-xs font-bold tracking-wider text-gray-400">
                <span class="hover:text-cyan-400 transition cursor-pointer" onclick="executeSecureAction(() => showToast('AI ස්ටූඩියෝව සක්‍රීයයි!'))">✨ AI ස්ටූඩියෝව</span>
                <span class="hover:text-cyan-400 transition cursor-pointer">ගීත එකතුව</span>
            </div>
            <div class="px-4 py-1.5 rounded-full bg-white/5 border border-white/10 text-[10px] font-bold text-gray-300 flex items-center space-x-2">
                <span class="w-2.5 h-2.5 rounded-full bg-cyan-400 animate-ping"></span>
                <span>GEMINI AI ACTIVE</span>
            </div>
        </div>
    </header>

    <!-- Main Container (ප්‍රධාන කොටස) -->
    <main class="flex-grow container mx-auto px-4 py-8 flex flex-col lg:flex-row gap-8 items-stretch max-w-7xl z-10">
        
        <!-- වම් පැත්ත: Music Player සහ Visualizer -->
        <div class="w-full lg:w-3/5 flex flex-col justify-between space-y-6">
            
            <!-- Dynamic Album Art / Visualizer Glass Panel -->
            <div class="glass-card rounded-[32px] p-8 flex flex-col items-center justify-center relative overflow-hidden h-[440px] transition-all duration-700" id="visualizer-container">
                
                <!-- Dynamic Blurred Cover Background -->
                <div class="absolute inset-0 z-0 opacity-20 pointer-events-none transition-all duration-700 overflow-hidden">
                    <img id="bg-blur-art" src="https://images.unsplash.com/photo-1514525253161-7a46d19cd819?auto=format&fit=crop&w=800&q=80" class="w-full h-full object-cover scale-125 blur-2xl">
                </div>

                <!-- Particle & Visualizer Canvas -->
                <canvas id="visualizer" class="absolute inset-0 w-full h-full opacity-80 pointer-events-none z-10"></canvas>

                <!-- High-Aesthetic Rotating Vinyl Interface -->
                <div class="relative z-20 flex flex-col items-center justify-center">
                    
                    <div class="relative group">
                        <div class="absolute -inset-2 bg-gradient-to-r from-cyan-400 via-pink-500 to-purple-600 rounded-full blur opacity-50 group-hover:opacity-100 transition duration-1000 group-hover:duration-200 animate-pulse"></div>
                        
                        <div class="relative w-56 h-56 rounded-full bg-neutral-950 border-[8px] border-neutral-900 flex items-center justify-center shadow-2xl spin-music spin-paused" id="vinyl-disc">
                            <div class="absolute inset-4 rounded-full border border-white/5"></div>
                            <div class="absolute inset-8 rounded-full border border-white/5"></div>
                            <div class="absolute inset-12 rounded-full border border-white/5"></div>
                            <div class="absolute inset-16 rounded-full border border-white/5"></div>
                            
                            <!-- High Quality Album Art Cover Photo -->
                            <div class="absolute inset-[48px] rounded-full overflow-hidden border-4 border-neutral-950">
                                <img id="album-art" src="https://images.unsplash.com/photo-1514525253161-7a46d19cd819?auto=format&fit=crop&w=500&q=80" alt="Album Cover" class="w-full h-full object-cover">
                            </div>
                            
                            <!-- Spindle Hole -->
                            <div class="absolute w-6 h-6 rounded-full bg-neutral-950 border-4 border-neutral-800 z-30 shadow-inner">
                                <div class="w-1 h-1 rounded-full bg-cyan-400 mx-auto mt-1.5"></div>
                            </div>
                        </div>
                    </div>

                    <!-- Glowing Track Meta Details -->
                    <div class="mt-8 text-center px-6 max-w-sm">
                        <h2 id="track-title" class="text-3xl font-extrabold tracking-wide truncate max-w-[280px] md:max-w-[380px] neon-glow-cyan transition-all duration-300 syne-font">සිංදුවක් තෝරන්න...</h2>
                        <p id="track-artist" class="text-[11px] tracking-[0.2em] text-gray-400 mt-2 uppercase font-black">GTK ENGINE AUDIO</p>
                    </div>
                </div>

                <!-- Waveform/Visualizer Mode Controllers -->
                <div class="absolute bottom-5 right-5 z-20 flex space-x-2 bg-black/50 p-1.5 rounded-2xl border border-white/10 backdrop-blur-md">
                    <button onclick="setVisualMode('circle')" id="btn-vis-circle" class="px-3.5 py-1.5 text-xs rounded-xl bg-cyan-500 text-black font-extrabold transition-all">Glow Circle</button>
                    <button onclick="setVisualMode('bars')" id="btn-vis-bars" class="px-3.5 py-1.5 text-xs rounded-xl text-gray-400 hover:text-white transition-all">Audio Bars</button>
                    <button onclick="setVisualMode('wave')" id="btn-vis-wave" class="px-3.5 py-1.5 text-xs rounded-xl text-gray-400 hover:text-white transition-all">Laser Wave</button>
                </div>
            </div>

            <!-- Sleek Interactive Controller Deck -->
            <div class="glass-card rounded-[32px] p-6 space-y-5 border-t border-cyan-400/20 shadow-2xl">
                
                <!-- Advanced Track Seeking Slider -->
                <div class="space-y-2">
                    <div class="flex justify-between text-[11px] text-gray-400 font-bold tracking-wider">
                        <span id="current-time" class="text-cyan-400">00:00</span>
                        <span id="duration-time" class="text-pink-500">00:00</span>
                    </div>
                    <div class="relative group h-2 bg-white/5 rounded-full cursor-pointer" id="progress-container">
                        <div class="absolute top-0 left-0 h-full bg-gradient-to-r from-cyan-400 via-pink-500 to-purple-600 rounded-full w-0" id="progress-bar"></div>
                        <div class="absolute top-1/2 -translate-y-1/2 -translate-x-1/2 w-4 h-4 bg-white border-2 border-cyan-400 rounded-full shadow-[0_0_15px_#00f3ff] opacity-0 group-hover:opacity-100 transition-opacity duration-200" id="progress-knob"></div>
                    </div>
                </div>

                <!-- Main Navigation Controls -->
                <div class="flex flex-col md:flex-row items-center justify-between gap-5 pt-1">
                    
                    <!-- Auxiliary (Shuffle/Repeat) buttons -->
                    <div class="flex items-center space-x-3.5 order-2 md:order-1">
                        <button id="btn-shuffle" onclick="executeSecureAction(toggleShuffle)" class="w-11 h-11 rounded-2xl bg-white/5 border border-white/5 flex items-center justify-center text-gray-400 hover:text-cyan-400 hover:bg-cyan-400/10 hover:border-cyan-400/30 transition-all duration-300" title="Shuffle">
                            <i class="fa-solid fa-shuffle text-sm"></i>
                        </button>
                        <button id="btn-repeat" onclick="executeSecureAction(toggleRepeat)" class="w-11 h-11 rounded-2xl bg-white/5 border border-white/5 flex items-center justify-center text-gray-400 hover:text-pink-500 hover:bg-pink-500/10 hover:border-pink-500/30 transition-all duration-300" title="Repeat">
                            <i class="fa-solid fa-repeat text-sm"></i>
                        </button>
                    </div>

                    <!-- Primary Player Engine Core buttons -->
                    <div class="flex items-center space-x-6 order-1 md:order-2">
                        <button onclick="executeSecureAction(prevTrack)" class="w-12 h-12 rounded-full bg-white/5 border border-white/5 hover:border-cyan-400/30 hover:bg-cyan-400/10 text-gray-300 hover:text-cyan-400 transition-all flex items-center justify-center active:scale-90" title="පෙර ගීතය">
                            <i class="fa-solid fa-backward-step text-lg"></i>
                        </button>
                        
                        <div class="relative">
                            <div class="absolute inset-0 bg-gradient-to-tr from-cyan-400 to-pink-500 rounded-full blur-xl opacity-70 animate-pulse" id="play-glow" style="display: none;"></div>
                            <button onclick="executeSecureAction(togglePlay)" id="btn-play-pause" class="relative w-[72px] h-[72px] rounded-full bg-gradient-to-tr from-cyan-400 via-fuchsia-500 to-pink-500 hover:scale-105 active:scale-95 transition-all flex items-center justify-center text-black text-2xl shadow-2xl button-glow" title="Play / Pause">
                                <i class="fa-solid fa-play ml-1.5" id="play-icon"></i>
                            </button>
                        </div>
                        
                        <button onclick="executeSecureAction(nextTrack)" class="w-12 h-12 rounded-full bg-white/5 border border-white/5 hover:border-cyan-400/30 hover:bg-cyan-400/10 text-gray-300 hover:text-cyan-400 transition-all flex items-center justify-center active:scale-90" title="මීළඟ ගීතය">
                            <i class="fa-solid fa-forward-step text-lg"></i>
                        </button>
                    </div>

                    <!-- Volume Controller deck -->
                    <div class="flex items-center space-x-3 w-full md:w-36 order-3 bg-white/5 px-3 py-2 rounded-2xl border border-white/5">
                        <button onclick="toggleMute()" class="text-gray-400 hover:text-cyan-400 transition-colors" id="btn-mute">
                            <i class="fa-solid fa-volume-high text-xs"></i>
                        </button>
                        <input type="range" id="volume-slider" min="0" max="1" step="0.05" value="0.7" class="w-full h-1 cursor-pointer accent-cyan-400">
                    </div>
                </div>

            </div>
        </div>

        <!-- දකුණු පැත්ත: AI Studio, Uploaders & Playlist -->
        <div class="w-full lg:w-2/5 flex flex-col space-y-6">
            
            <!-- ✨ GEMINI AI INTUITIVE STUDIO PANEL -->
            <div class="glass-card rounded-[32px] p-6 border border-cyan-400/30 shadow-[0_0_20px_rgba(0,243,255,0.1)] relative overflow-hidden">
                <div class="absolute -top-10 -right-10 w-24 h-24 bg-cyan-400/10 rounded-full blur-xl"></div>
                <h3 class="text-lg font-bold tracking-wider flex items-center space-x-2 syne-font mb-4 text-cyan-400">
                    <i class="fa-solid fa-wand-magic-sparkles"></i>
                    <span>GTK ✨ AI ස්ටූඩියෝව</span>
                </h3>
                
                <!-- AI Mood Composer Interface -->
                <div class="space-y-4">
                    <div>
                        <label class="block text-xs text-gray-400 font-bold mb-1.5">ඔබේ මනෝභාවය (Mood / Scenario) ලියන්න:</label>
                        <div class="flex gap-2">
                            <input type="text" id="ai-mood-input" placeholder="उदा: Colombo rainy midnight, neon gaming hype..." class="flex-grow bg-white/5 border border-white/10 rounded-xl px-4 py-2.5 text-sm focus:outline-none focus:border-cyan-400 transition text-gray-100">
                            <button onclick="executeSecureAction(generateAiMoodBeat)" id="btn-generate-ai" class="bg-gradient-to-r from-cyan-400 to-purple-600 hover:from-cyan-300 hover:to-purple-500 text-black font-extrabold text-xs px-4 py-2.5 rounded-xl transition duration-300 shadow-lg shadow-cyan-500/10 active:scale-95 flex items-center gap-1.5 flex-shrink-0">
                                <i class="fa-solid fa-microchip"></i>
                                <span>✨ Beat එක හදන්න</span>
                            </button>
                        </div>
                    </div>

                    <!-- Lyric & Interpretation Engine Trigger -->
                    <div class="pt-3 border-t border-white/5 flex justify-between items-center">
                        <span class="text-xs text-gray-400">වත්මන් ගීතයේ පද සහ තේරුම:</span>
                        <button onclick="executeSecureAction(generateSongLyricsAndMeaning)" class="px-4 py-2 text-xs bg-pink-500/10 border border-pink-400/30 text-pink-400 hover:bg-pink-500/20 rounded-xl font-bold transition flex items-center gap-1.5">
                            <i class="fa-solid fa-pen-nib"></i>
                            <span>✨ පද සහ තේරුම ලියන්න</span>
                        </button>
                    </div>
                </div>

                <!-- AI Response display panel -->
                <div id="ai-response-panel" class="hidden mt-4 p-4 rounded-2xl bg-black/40 border border-white/5 max-h-[180px] overflow-y-auto text-xs space-y-2">
                    <h4 id="ai-response-title" class="font-bold text-cyan-400 border-b border-white/5 pb-1">AI Output</h4>
                    <p id="ai-response-content" class="text-gray-300 leading-relaxed whitespace-pre-line"></p>
                </div>
            </div>

            <!-- Drag-Drop MP3 Uploader Zone -->
            <div class="glass-card rounded-[32px] p-5 relative group border-dashed border-2 border-white/10 hover:border-cyan-400/50 hover:bg-cyan-500/5 transition-all duration-500">
                <input type="file" id="file-input" accept="audio/mp3, audio/*" multiple class="hidden">
                <div class="flex flex-col items-center justify-center text-center cursor-pointer py-4" onclick="executeSecureAction(() => document.getElementById('file-input').click())">
                    <div class="relative mb-2">
                        <div class="relative w-12 h-12 rounded-2xl bg-cyan-500/10 border border-cyan-500/20 flex items-center justify-center text-cyan-400 group-hover:scale-110 group-hover:text-cyan-300 transition-all duration-300">
                            <i class="fa-solid fa-cloud-arrow-up text-2xl"></i>
                        </div>
                    </div>
                    <h3 class="text-sm font-bold tracking-wide syne-font text-gray-200">ඔබේ MP3 ගීත මෙතැනට දාන්න</h3>
                    <p class="text-[10px] text-gray-400 mt-1 px-4 leading-relaxed">මෙතැන ක්ලික් කර හෝ ගොනු Drag & Drop කර ඔබේ ප්‍රියතම සිංදු එකතු කරන්න.</p>
                </div>
            </div>

            <!-- Curated High Contrast Playlist View -->
            <div class="glass-card rounded-[32px] p-6 flex-grow flex flex-col justify-between min-h-[300px] border-t border-pink-500/10">
                <div>
                    <div class="flex justify-between items-center mb-4">
                        <h3 class="text-lg font-bold tracking-wider flex items-center space-x-3 syne-font">
                            <span class="inline-block w-2.5 h-2.5 rounded-full bg-pink-500 shadow-[0_0_10px_#ff007f] animate-pulse"></span>
                            <span>මගේ සංගීත ලැයිස්තුව</span>
                        </h3>
                        <span id="playlist-count" class="text-[10px] bg-cyan-400/15 border border-cyan-400/20 px-3 py-1 rounded-full text-cyan-400 font-bold">0 TRACKS</span>
                    </div>

                    <!-- Scrolling container for files -->
                    <div id="playlist-container" class="space-y-2 max-h-[200px] overflow-y-auto pr-1">
                        <div id="no-songs" class="text-center py-12 text-gray-500">
                            <i class="fa-solid fa-compact-disc text-4xl mb-3 block opacity-20 spin-music"></i>
                            <p class="text-xs font-bold text-gray-400">තවමත් ගීත එකතු කර නොමැත.</p>
                            <p class="text-[10px] text-gray-500 mt-1">ඔබේම MP3 ගොනු දමන්න, නැතහොත් පහත බොත්තමෙන් Demo Synth Beat එක අසන්න.</p>
                            
                            <button onclick="executeSecureAction(loadDemoBeat)" class="mt-4 px-5 py-2 text-[10px] bg-gradient-to-r from-pink-500 to-purple-600 hover:from-pink-400 hover:to-purple-500 text-white font-black tracking-wider rounded-full shadow-[0_0_10px_rgba(255,0,127,0.3)] transition-all">
                                DEMO SYNTH BEAT එකක් අහන්න ⚡
                            </button>
                        </div>
                    </div>
                </div>

                <!-- Custom Actions & Brand Info -->
                <div class="pt-3 border-t border-white/5 mt-4 flex justify-between items-center text-xs">
                    <button onclick="executeSecureAction(clearPlaylist)" class="text-red-400 hover:text-red-300 flex items-center space-x-2 transition font-bold">
                        <i class="fa-solid fa-trash-can"></i>
                        <span>සංගීත එකතුව මකන්න (Clear)</span>
                    </button>
                    <span class="text-gray-600 font-bold">GEMINI GENERATIVE v2.5</span>
                </div>
            </div>

        </div>

    </main>

    <!-- Footer -->
    <footer class="w-full py-5 text-center text-[10px] text-gray-500 glass-card border-t border-white/5 mt-8 tracking-widest uppercase font-bold">
        <p>© 2026 GTK MUSIC HUB. ULTRA PREMIUM EXPERIENCE WITH ✨ GEMINI AI</p>
    </footer>

    <!-- Glowing Custom Password Modal Screen -->
    <div id="password-modal" class="fixed inset-0 bg-black/85 backdrop-blur-md hidden items-center justify-center z-50 transition-all duration-300">
        <div class="glass-card rounded-[32px] p-8 max-w-sm w-full mx-4 border border-cyan-400/40 shadow-[0_0_50px_rgba(0,243,255,0.2)] text-center space-y-6">
            <div class="w-16 h-16 bg-cyan-500/10 rounded-2xl border border-cyan-500/20 flex items-center justify-center text-cyan-400 mx-auto animate-pulse">
                <i class="fa-solid fa-lock text-3xl"></i>
            </div>
            <div>
                <h3 class="text-xl font-bold tracking-wider syne-font text-gray-200">GTK SECURITY LOCK</h3>
                <p class="text-xs text-gray-400 mt-2">මෙම ක්‍රියාව සිදු කිරීමට කරුණාකර මුරපදය (Password) ඇතුළත් කරන්න.</p>
            </div>
            <div class="space-y-4">
                <div class="relative">
                    <input type="password" id="app-password-input" placeholder="Password එක ලියන්න..." class="w-full bg-white/5 border border-white/10 rounded-xl px-4 py-3 pr-10 text-sm text-center focus:outline-none focus:border-cyan-400 transition text-gray-100">
                    <button type="button" onclick="togglePasswordVisibility()" class="absolute right-3 top-1/2 -translate-y-1/2 text-gray-400 hover:text-cyan-400 transition-colors">
                        <i class="fa-solid fa-eye-slash" id="eye-icon"></i>
                    </button>
                </div>
                <button onclick="verifyLockPassword()" class="w-full bg-gradient-to-r from-cyan-400 to-purple-600 text-black font-extrabold text-sm py-3 rounded-xl hover:scale-[1.02] active:scale-95 transition-all">
                    UNLOCK ENGINE 🔓
                </button>
                <button onclick="closePasswordModal()" class="text-xs text-gray-500 hover:text-gray-400 font-bold block mx-auto">අවලංගු කරන්න (Cancel)</button>
            </div>
        </div>
    </div>

    <!-- Audio Player -->
    <audio id="audio-player"></audio>

    <!-- Notification Toast -->
    <div id="toast" class="fixed bottom-6 right-6 transform translate-y-24 opacity-0 glass-card border-cyan-400/40 text-cyan-400 px-6 py-4 rounded-2xl flex items-center space-x-3.5 transition-all duration-300 shadow-[0_15px_30px_rgba(0,0,0,0.5)] z-50">
        <div class="w-7 h-7 rounded-full bg-cyan-400/20 flex items-center justify-center">
            <i class="fa-solid fa-bolt text-xs"></i>
        </div>
        <span id="toast-msg" class="text-xs font-black tracking-wider">SUCCESSFUL!</span>
    </div>

    <!-- JS Core Player logic implementation -->
    <script>
        const apiKey = ""; // Gemini API Key is provided by runtime environment

        let playlist = [];
        let currentTrackIndex = -1;
        let isPlaying = false;
        let isShuffle = false;
        let isRepeat = false;
        let visualMode = 'circle'; 

        // Password Security variables
        let isUnlocked = false; 
        const correctPassword = "GTK@2026"; 
        let pendingAction = null;

        // Web Audio API context handles
        let audioCtx;
        let audioSource;
        let analyser;
        let animationId;
        
        // Particle system storage
        let particles = [];

        // Curated photography covers
        const aestheticCovers = [
            'https://images.unsplash.com/photo-1514525253161-7a46d19cd819?auto=format&fit=crop&w=500&q=80',
            'https://images.unsplash.com/photo-1470225620780-dba8ba36b745?auto=format&fit=crop&w=500&q=80',
            'https://images.unsplash.com/photo-1508700115892-45ecd05ae2ad?auto=format&fit=crop&w=500&q=80',
            'https://images.unsplash.com/photo-1511671782779-c97d3d27a1d4?auto=format&fit=crop&w=500&q=80',
            'https://images.unsplash.com/photo-1614613535308-eb5fbd3d2c17?auto=format&fit=crop&w=500&q=80'
        ];

        // Core DOM Selectors
        const audioPlayer = document.getElementById('audio-player');
        const playBtn = document.getElementById('btn-play-pause');
        const playIcon = document.getElementById('play-icon');
        const playGlow = document.getElementById('play-glow');
        const vinylDisc = document.getElementById('vinyl-disc');
        const logoDisc = document.getElementById('logo-disc');
        const albumArt = document.getElementById('album-art');
        const bgBlurArt = document.getElementById('bg-blur-art');
        const trackTitle = document.getElementById('track-title');
        const trackArtist = document.getElementById('track-artist');
        const progressContainer = document.getElementById('progress-container');
        const progressBar = document.getElementById('progress-bar');
        const progressKnob = document.getElementById('progress-knob');
        const currentTimeEl = document.getElementById('current-time');
        const durationTimeEl = document.getElementById('duration-time');
        const volumeSlider = document.getElementById('volume-slider');
        const btnMute = document.getElementById('btn-mute');
        const fileInput = document.getElementById('file-input');
        const playlistContainer = document.getElementById('playlist-container');
        const playlistCount = document.getElementById('playlist-count');
        const noSongsMsg = document.getElementById('no-songs');
        const canvas = document.getElementById('visualizer');
        const canvasCtx = canvas.getContext('2d');

        function resizeCanvas() {
            canvas.width = canvas.parentElement.clientWidth;
            canvas.height = canvas.parentElement.clientHeight;
        }
        window.addEventListener('resize', resizeCanvas);
        resizeCanvas();

        // --- PASSWORD SECURITY CORE ACTIONS ---
        function executeSecureAction(action) {
            if (isUnlocked) {
                action();
            } else {
                pendingAction = action;
                openPasswordModal();
            }
        }

        function openPasswordModal() {
            const modal = document.getElementById('password-modal');
            modal.classList.remove('hidden');
            modal.classList.add('flex');
            document.getElementById('app-password-input').focus();
        }

        function closePasswordModal() {
            const modal = document.getElementById('password-modal');
            modal.classList.remove('flex');
            modal.classList.add('hidden');
            document.getElementById('app-password-input').value = "";
            
            // Close කරන විට සැමවිටම password type එක reset කිරීම
            const pwdInput = document.getElementById('app-password-input');
            pwdInput.type = 'password';
            document.getElementById('eye-icon').className = 'fa-solid fa-eye-slash';
            
            pendingAction = null;
        }

        function togglePasswordVisibility() {
            const pwdInput = document.getElementById('app-password-input');
            const eyeIcon = document.getElementById('eye-icon');
            if (pwdInput.type === 'password') {
                pwdInput.type = 'text';
                eyeIcon.className = 'fa-solid fa-eye';
            } else {
                pwdInput.type = 'password';
                eyeIcon.className = 'fa-solid fa-eye-slash';
            }
        }

        function verifyLockPassword() {
            const userInput = document.getElementById('app-password-input').value;
            if (userInput === correctPassword) {
                isUnlocked = true;
                showToast("GTK ENGINE UNLOCKED SUCCESSFULLY! 🔓");
                closePasswordModal();
                if (pendingAction) {
                    pendingAction();
                    pendingAction = null;
                }
            } else {
                showToast("වැරදි මුරපදයක්! කරුණාකර නැවත උත්සාහ කරන්න. ❌");
                document.getElementById('app-password-input').value = "";
            }
        }

        // Handle Enter key inside password modal input
        document.getElementById('app-password-input').addEventListener('keypress', (e) => {
            if (e.key === 'Enter') {
                verifyLockPassword();
            }
        });

        // --- File Uploader Processing logic ---
        fileInput.addEventListener('change', (e) => {
            const files = Array.from(e.target.files);
            if (files.length === 0) return;

            files.forEach(file => {
                let title = file.name.replace(/\.[^/.]+$/, "");
                let artist = "MP3 AUDIO FILE";
                
                if (title.includes('-')) {
                    const parts = title.split('-');
                    artist = parts[0].trim();
                    title = parts[1].trim();
                }

                const cover = aestheticCovers[playlist.length % aestheticCovers.length];

                const track = {
                    title: title,
                    artist: artist,
                    url: URL.createObjectURL(file),
                    cover: cover
                };

                playlist.push(track);
            });

            showToast(`${files.length} TRACKS ADDED TO GTK ENGINE! ⚡`);
            updatePlaylistUI();
            
            if (currentTrackIndex === -1 && playlist.length > 0) {
                loadTrack(0);
            }
        });

        // Drag & Drop event wrappers
        const dropZone = fileInput.parentElement;
        ['dragenter', 'dragover'].forEach(name => {
            dropZone.addEventListener(name, (e) => {
                e.preventDefault();
                dropZone.classList.add('border-cyan-400', 'bg-cyan-500/10');
            });
        });
        ['dragleave', 'drop'].forEach(name => {
            dropZone.addEventListener(name, (e) => {
                e.preventDefault();
                dropZone.classList.remove('border-cyan-400', 'bg-cyan-500/10');
            });
        });
        dropZone.addEventListener('drop', (e) => {
            e.preventDefault();
            dropZone.classList.remove('border-cyan-400', 'bg-cyan-500/10');
            
            const dt = e.dataTransfer;
            const files = dt.files;
            if (files.length > 0) {
                executeSecureAction(() => {
                    fileInput.files = files;
                    fileInput.dispatchEvent(new Event('change'));
                });
            }
        });

        // --- Playlist UI Drawing ---
        function updatePlaylistUI() {
            playlistCount.textContent = `${playlist.length} TRACKS`;
            
            if (playlist.length === 0) {
                noSongsMsg.style.display = 'block';
                playlistContainer.querySelectorAll('.track-item').forEach(el => el.remove());
                return;
            }

            noSongsMsg.style.display = 'none';
            playlistContainer.querySelectorAll('.track-item').forEach(el => el.remove());

            playlist.forEach((track, index) => {
                const trackItem = document.createElement('div');
                trackItem.className = `track-item p-3 rounded-2xl flex items-center justify-between cursor-pointer transition-all duration-300 group/item ${index === currentTrackIndex ? 'bg-gradient-to-r from-cyan-400/15 to-pink-500/5 border border-cyan-400/30 shadow-lg shadow-cyan-950/20' : 'hover:bg-white/5 border border-transparent'}`;
                trackItem.innerHTML = `
                    <div class="flex items-center space-x-3.5 overflow-hidden w-3/5" onclick="executeSecureAction(() => selectTrack(${index}))">
                        <div class="relative w-11 h-11 rounded-xl overflow-hidden bg-neutral-900 flex-shrink-0 border border-white/5 flex items-center justify-center">
                            <img src="${track.cover}" class="w-full h-full object-cover group-hover/item:scale-110 transition duration-350">
                            ${index === currentTrackIndex && isPlaying ? '<div class="absolute inset-0 bg-black/60 flex items-center justify-center"><i class="fa-solid fa-volume-high text-cyan-400 animate-pulse text-xs"></i></div>' : ''}
                        </div>
                        <div class="overflow-hidden">
                            <h4 class="text-sm font-bold truncate ${index === currentTrackIndex ? 'text-cyan-400 neon-glow-cyan' : 'text-gray-200'}">${track.title}</h4>
                            <p class="text-[10px] text-gray-400 mt-0.5 truncate tracking-wide uppercase font-bold">${track.artist}</p>
                        </div>
                    </div>
                    <!-- Controls section including Download (UNLOCKED) and Delete (LOCKED) -->
                    <div class="flex items-center space-x-2">
                        <button onclick="downloadTrack(${index}, event)" class="p-2.5 bg-cyan-400/10 hover:bg-cyan-400/20 text-cyan-400 rounded-xl transition duration-300" title="ඩවුන්ලෝඩ් කරන්න (බාගන්න)">
                            <i class="fa-solid fa-download text-xs"></i>
                        </button>
                        <button onclick="executeSecureAction(() => removeTrack(${index}, event))" class="opacity-0 group-hover/item:opacity-100 p-2.5 text-gray-500 hover:text-red-400 transition" title="ඉවත් කරන්න">
                            <i class="fa-solid fa-trash-can text-xs"></i>
                        </button>
                    </div>
                `;
                playlistContainer.appendChild(trackItem);
            });
        }

        // --- Unlocked track downloading feature ---
        function downloadTrack(index, event) {
            event.stopPropagation();
            const track = playlist[index];
            const a = document.createElement('a');
            a.href = track.url;
            a.download = `${track.title} - ${track.artist}.wav`;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            showToast("DOWNLOADING TRACK... 📥");
        }

        // --- Music loading and playback operations ---
        function loadTrack(index) {
            if (index < 0 || index >= playlist.length) return;
            
            currentTrackIndex = index;
            const track = playlist[index];
            
            audioPlayer.src = track.url;
            audioPlayer.load();

            trackTitle.textContent = track.title;
            trackArtist.textContent = track.artist;
            albumArt.src = track.cover;
            bgBlurArt.src = track.cover;

            const isEven = index % 2 === 0;
            const container = document.getElementById('visualizer-container');
            if (isEven) {
                container.classList.add('glow-cyan');
                container.classList.remove('glow-magenta');
                trackTitle.className = "text-3xl font-extrabold tracking-wide truncate max-w-[280px] md:max-w-[380px] neon-glow-cyan transition-all duration-300 syne-font";
            } else {
                container.classList.add('glow-magenta');
                container.classList.remove('glow-cyan');
                trackTitle.className = "text-3xl font-extrabold tracking-wide truncate max-w-[280px] md:max-w-[380px] neon-glow-pink transition-all duration-300 syne-font";
            }

            updatePlaylistUI();
            initAudioContext();
        }

        function togglePlay() {
            if (playlist.length === 0) {
                showToast("කරුණාකර පළමුව MP3 ගීතයක් එකතු කරන්න!");
                return;
            }
            if (isPlaying) {
                pauseTrack();
            } else {
                playTrack();
            }
        }

        function playTrack() {
            if (audioCtx && audioCtx.state === 'suspended') {
                audioCtx.resume();
            }
            audioPlayer.play().then(() => {
                isPlaying = true;
                playIcon.className = "fa-solid fa-pause text-black";
                playGlow.style.display = 'block';
                vinylDisc.classList.remove('spin-paused');
                logoDisc.classList.remove('spin-paused');
                updatePlaylistUI();
                startVisualizer();
            }).catch(e => console.log(e));
        }

        function pauseTrack() {
            audioPlayer.pause();
            isPlaying = false;
            playIcon.className = "fa-solid fa-play ml-1.5 text-black";
            playGlow.style.display = 'none';
            vinylDisc.classList.add('spin-paused');
            logoDisc.classList.add('spin-paused');
            updatePlaylistUI();
        }

        function nextTrack() {
            if (playlist.length === 0) return;
            if (isShuffle) {
                loadTrack(Math.floor(Math.random() * playlist.length));
            } else {
                let next = currentTrackIndex + 1 >= playlist.length ? 0 : currentTrackIndex + 1;
                loadTrack(next);
            }
            playTrack();
        }

        function prevTrack() {
            if (playlist.length === 0) return;
            let prev = currentTrackIndex - 1 < 0 ? playlist.length - 1 : currentTrackIndex - 1;
            loadTrack(prev);
            playTrack();
        }

        function selectTrack(index) {
            loadTrack(index);
            playTrack();
        }

        function removeTrack(index, event) {
            if (event) event.stopPropagation();
            if (playlist[index].url.startsWith('blob:')) {
                URL.revokeObjectURL(playlist[index].url);
            }
            playlist.splice(index, 1);
            if (currentTrackIndex === index) {
                if (playlist.length > 0) {
                    loadTrack(index >= playlist.length ? 0 : index);
                    if (isPlaying) playTrack();
                } else {
                    resetStateToBlank();
                }
            } else if (currentTrackIndex > index) {
                currentTrackIndex--;
            }
            showToast("TRACK REMOVED");
            updatePlaylistUI();
        }

        function clearPlaylist() {
            playlist.forEach(t => {
                if (t.url.startsWith('blob:')) URL.revokeObjectURL(t.url);
            });
            playlist = [];
            resetStateToBlank();
            showToast("PLAYLIST CLEARED! 🧹");
            updatePlaylistUI();
        }

        function resetStateToBlank() {
            audioPlayer.src = '';
            currentTrackIndex = -1;
            isPlaying = false;
            playIcon.className = "fa-solid fa-play ml-1.5 text-black";
            playGlow.style.display = 'none';
            vinylDisc.classList.add('spin-paused');
            logoDisc.classList.add('spin-paused');
            trackTitle.textContent = "සිංදුවක් තෝරන්න...";
            trackArtist.textContent = "GTK ENGINE AUDIO";
            albumArt.src = 'https://images.unsplash.com/photo-1514525253161-7a46d19cd819?auto=format&fit=crop&w=500&q=80';
            bgBlurArt.src = 'https://images.unsplash.com/photo-1514525253161-7a46d19cd819?auto=format&fit=crop&w=500&q=80';
        }

        function toggleShuffle() {
            isShuffle = !isShuffle;
            const btn = document.getElementById('btn-shuffle');
            if (isShuffle) {
                btn.className = "w-11 h-11 rounded-2xl bg-cyan-400/10 border border-cyan-400/40 flex items-center justify-center text-cyan-400 shadow-[0_0_15px_rgba(0,243,255,0.3)]";
                showToast("SHUFFLE PLAYLIST ENABLED 🔀");
            } else {
                btn.className = "w-11 h-11 rounded-2xl bg-white/5 border border-white/5 flex items-center justify-center text-gray-400 hover:text-cyan-400";
            }
        }

        function toggleRepeat() {
            isRepeat = !isRepeat;
            const btn = document.getElementById('btn-repeat');
            if (isRepeat) {
                btn.className = "w-11 h-11 rounded-2xl bg-pink-500/10 border border-pink-500/40 flex items-center justify-center text-pink-500 shadow-[0_0_15px_rgba(255,0,127,0.3)]";
                audioPlayer.loop = true;
                showToast("LOOP CURRENT TRACK ENABLED 🔁");
            } else {
                btn.className = "w-11 h-11 rounded-2xl bg-white/5 border border-white/5 flex items-center justify-center text-gray-400 hover:text-pink-500";
                audioPlayer.loop = false;
            }
        }

        // Seek Tracking
        audioPlayer.addEventListener('timeupdate', () => {
            const current = audioPlayer.currentTime;
            const duration = audioPlayer.duration || 0;
            const pct = (current / duration) * 100;
            progressBar.style.width = `${pct}%`;
            progressKnob.style.left = `${pct}%`;
            currentTimeEl.textContent = formatTime(current);
            durationTimeEl.textContent = isNaN(duration) ? "00:00" : formatTime(duration);
        });

        audioPlayer.addEventListener('ended', () => {
            if (!isRepeat) nextTrack();
        });

        function formatTime(secs) {
            const m = Math.floor(secs / 60);
            const s = Math.floor(secs % 60);
            return `${m < 10 ? '0' : ''}${m}:${s < 10 ? '0' : ''}${s}`;
        }

        progressContainer.addEventListener('click', (e) => {
            executeSecureAction(() => {
                const w = progressContainer.clientWidth;
                const x = e.offsetX;
                const d = audioPlayer.duration || 0;
                audioPlayer.currentTime = (x / w) * d;
            });
        });

        volumeSlider.addEventListener('input', (e) => {
            audioPlayer.volume = e.target.value;
            updateVolumeIcon(e.target.value);
        });

        function updateVolumeIcon(val) {
            if (val == 0) {
                btnMute.innerHTML = '<i class="fa-solid fa-volume-xmark text-red-500"></i>';
            } else if (val < 0.4) {
                btnMute.innerHTML = '<i class="fa-solid fa-volume-low text-cyan-400"></i>';
            } else {
                btnMute.innerHTML = '<i class="fa-solid fa-volume-high text-cyan-400"></i>';
            }
        }

        function toggleMute() {
            if (audioPlayer.muted) {
                audioPlayer.muted = false;
                volumeSlider.value = audioPlayer.volume;
                updateVolumeIcon(audioPlayer.volume);
            } else {
                audioPlayer.muted = true;
                volumeSlider.value = 0;
                btnMute.innerHTML = '<i class="fa-solid fa-volume-xmark text-red-500"></i>';
            }
        }

        // --- Audio Context & Complex Particle Visualizer Core ---
        function initAudioContext() {
            if (audioCtx) return;
            audioCtx = new (window.AudioContext || window.webkitAudioContext)();
            analyser = audioCtx.createAnalyser();
            audioSource = audioCtx.createMediaElementSource(audioPlayer);
            audioSource.connect(analyser);
            analyser.connect(audioCtx.destination);
            analyser.fftSize = 256;
            
            createParticles();
        }

        function setVisualMode(mode) {
            visualMode = mode;
            ['bars', 'wave', 'circle'].forEach(m => {
                const btn = document.getElementById(`btn-vis-${m}`);
                if (m === mode) {
                    btn.className = "px-3.5 py-1.5 text-xs rounded-xl bg-cyan-500 text-black font-extrabold transition-all";
                } else {
                    btn.className = "px-3.5 py-1.5 text-xs rounded-xl text-gray-400 hover:text-white transition-all";
                }
            });
        }

        function createParticles() {
            particles = [];
            for (let i = 0; i < 40; i++) {
                particles.push({
                    x: Math.random() * canvas.width,
                    y: Math.random() * canvas.height + canvas.height,
                    size: Math.random() * 2.5 + 0.5,
                    speedY: Math.random() * 1.5 + 0.2,
                    alpha: Math.random() * 0.5 + 0.1
                });
            }
        }

        function startVisualizer() {
            if (!analyser) return;
            const bufferLen = analyser.frequencyBinCount;
            const dataArray = new Uint8Array(bufferLen);

            function draw() {
                if (!isPlaying) {
                    cancelAnimationFrame(animationId);
                    return;
                }
                animationId = requestAnimationFrame(draw);
                analyser.getByteFrequencyData(dataArray);
                
                canvasCtx.fillStyle = 'rgba(3, 0, 10, 0.2)';
                canvasCtx.fillRect(0, 0, canvas.width, canvas.height);

                let sum = 0;
                for (let i = 0; i < bufferLen; i++) {
                    sum += dataArray[i];
                }
                const averageVolume = sum / bufferLen;

                particles.forEach(p => {
                    p.y -= p.speedY + (averageVolume / 30); 
                    if (p.y < -10) {
                        p.y = canvas.height + 10;
                        p.x = Math.random() * canvas.width;
                    }
                    canvasCtx.beginPath();
                    canvasCtx.arc(p.x, p.y, p.size, 0, Math.PI * 2);
                    canvasCtx.fillStyle = `rgba(0, 243, 255, ${p.alpha})`;
                    canvasCtx.fill();
                });

                if (visualMode === 'bars') {
                    const barWidth = (canvas.width / bufferLen) * 1.4;
                    let x = 0;
                    for (let i = 0; i < bufferLen; i++) {
                        const barHeight = dataArray[i] * 1.2;
                        const grad = canvasCtx.createLinearGradient(0, canvas.height, 0, canvas.height - barHeight);
                        grad.addColorStop(0, 'rgba(112, 0, 255, 0.05)');
                        grad.addColorStop(0.5, 'rgba(255, 0, 127, 0.4)');
                        grad.addColorStop(1, '#00f3ff');

                        canvasCtx.fillStyle = grad;
                        canvasCtx.fillRect(x, canvas.height - barHeight, barWidth - 3, barHeight);
                        x += barWidth;
                    }
                } else if (visualMode === 'wave') {
                    analyser.getByteTimeDomainData(dataArray);
                    canvasCtx.lineWidth = 3;
                    const grad = canvasCtx.createLinearGradient(0, 0, canvas.width, 0);
                    grad.addColorStop(0, '#ff007f');
                    grad.addColorStop(0.5, '#00f3ff');
                    grad.addColorStop(1, '#7000ff');
                    canvasCtx.strokeStyle = grad;
                    canvasCtx.beginPath();
                    
                    const sliceW = canvas.width * 1.0 / bufferLen;
                    let x = 0;
                    for (let i = 0; i < bufferLen; i++) {
                        const v = dataArray[i] / 128.0;
                        const y = (v * canvas.height / 2) + (Math.sin(i / 10) * (averageVolume / 10)); 
                        if (i === 0) canvasCtx.moveTo(x, y);
                        else canvasCtx.lineTo(x, y);
                        x += sliceW;
                    }
                    canvasCtx.lineTo(canvas.width, canvas.height / 2);
                    canvasCtx.stroke();
                } else if (visualMode === 'circle') {
                    const cx = canvas.width / 2;
                    const cy = canvas.height / 2;
                    const baseRadius = 120;

                    for (let i = 0; i < bufferLen; i += 2) {
                        const angle = (i / bufferLen) * Math.PI * 2;
                        const val = dataArray[i] / 2.5;
                        const r1 = baseRadius;
                        const r2 = baseRadius + val;

                        const x1 = cx + Math.cos(angle) * r1;
                        const y1 = cy + Math.sin(angle) * r1;
                        const x2 = cx + Math.cos(angle) * r2;
                        const y2 = cy + Math.sin(angle) * r2;

                        const grad = canvasCtx.createLinearGradient(x1, y1, x2, y2);
                        grad.addColorStop(0, '#ff007f');
                        grad.addColorStop(1, '#00f3ff');

                        canvasCtx.strokeStyle = grad;
                        canvasCtx.lineWidth = 3.5;
                        canvasCtx.beginPath();
                        canvasCtx.moveTo(x1, y1);
                        canvasCtx.lineTo(x2, y2);
                        canvasCtx.stroke();
                    }
                }
            }
            draw();
        }

        // --- Demo Sound Beat Generator ---
        function loadDemoBeat() {
            showToast("GENERATING RETRO SYNTH BEAT...");
            const sampleRate = 44100;
            const duration = 12;
            const numSamples = sampleRate * duration;
            const audioBuffer = new Float32Array(numSamples);
            
            for (let i = 0; i < numSamples; i++) {
                const t = i / sampleRate;
                const kick = Math.sin(2 * Math.PI * 55 * Math.exp(-t * 7 % 1)) * Math.exp(-t * 6 % 1);
                
                const bassFrequencies = [110, 110, 146, 165, 130, 130, 165, 196];
                const measure = Math.floor(t * 3.5) % bassFrequencies.length;
                const freq = bassFrequencies[measure];
                const synthBass = Math.sin(2 * Math.PI * freq * t) * 0.18 * Math.exp(-t * 3.5 % 1);
                
                const melodyFrequencies = [440, 523, 587, 659, 784];
                const melodyMeasure = Math.floor(t * 1.5) % melodyFrequencies.length;
                const leadFreq = melodyFrequencies[melodyMeasure];
                const synthLead = Math.sin(2 * Math.PI * leadFreq * t) * 0.08 * Math.exp(-t * 2 % 1);
                
                audioBuffer[i] = (kick * 0.55 + synthBass + synthLead) * 0.35;
            }

            const binaryWav = createWavBinary(audioBuffer, sampleRate);
            const blob = new Blob([binaryWav], { type: 'audio/wav' });
            const url = URL.createObjectURL(blob);

            playlist.push({
                title: "GTK Celestial Synthwave",
                artist: "GTK ARTIFICIAL SYNTH v4",
                url: url,
                cover: 'https://images.unsplash.com/photo-1614613535308-eb5fbd3d2c17?auto=format&fit=crop&w=500&q=80'
            });

            updatePlaylistUI();
            loadTrack(playlist.length - 1);
            playTrack();
            showToast("SYNTH BEAT GENERATED! ⚡");
        }

        // WAV formulation helper
        function createWavBinary(samples, sampleRate) {
            const buffer = new ArrayBuffer(44 + samples.length * 2);
            const view = new DataView(buffer);
            writeString(view, 0, 'RIFF');
            view.setUint32(4, 36 + samples.length * 2, true);
            writeString(view, 8, 'WAVE');
            writeString(view, 12, 'fmt ');
            view.setUint32(16, 16, true);
            view.setUint16(20, 1, true);
            view.setUint16(22, 1, true);
            view.setUint32(24, sampleRate, true);
            view.setUint32(28, sampleRate * 2, true);
            view.setUint16(32, 2, true);
            view.setUint16(34, 16, true);
            writeString(view, 36, 'data');
            view.setUint32(40, samples.length * 2, true);

            let offset = 44;
            for (let i = 0; i < samples.length; i++, offset += 2) {
                const s = Math.max(-1, Math.min(1, samples[i]));
                view.setInt16(offset, s < 0 ? s * 0x8000 : s * 0x7FFF, true);
            }
            return buffer;
        }

        function writeString(view, offset, string) {
            for (let i = 0; i < string.length; i++) {
                view.setUint8(offset + i, string.charCodeAt(i));
            }
        }

        // --- GEMINI INTEGRATIONS ---

        async function robustFetchGemini(prompt, systemPrompt, schema = null) {
            const model = "gemini-2.5-flash-preview-09-2025";
            const url = `https://generativelanguage.googleapis.com/v1beta/models/${model}:generateContent?key=${apiKey}`;
            
            const payload = {
                contents: [{ parts: [{ text: prompt }] }],
                systemInstruction: { parts: [{ text: systemPrompt }] }
            };

            if (schema) {
                payload.generationConfig = {
                    responseMimeType: "application/json",
                    responseSchema: schema
                };
            }

            let delay = 1000;
            for (let attempt = 0; attempt < 5; attempt++) {
                try {
                    const response = await fetch(url, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify(payload)
                    });
                    if (response.ok) {
                        return await response.json();
                    }
                } catch (e) {
                    // Fail silently inside backoff
                }
                await new Promise(r => setTimeout(r, delay));
                delay *= 2;
            }
            throw new Error("Gemini AI සේවාව වෙත සම්බන්ධ වීමට අපොහොසත් විය. කරුණාකර ඔබගේ අන්තර්ජාල සම්බන්ධතාවය පරීක්ෂා කරන්න.");
        }

        // Feature 1: ✨ AI Mood Beat Creator
        async function generateAiMoodBeat() {
            const moodInput = document.getElementById('ai-mood-input').value.trim();
            if (!moodInput) {
                showToast("කරුණාකර යම් මූඩ් එකක් හෝ අදහසක් ලියන්න!");
                return;
            }

            const btn = document.getElementById('btn-generate-ai');
            const originalHtml = btn.innerHTML;
            btn.innerHTML = `<i class="fa-solid fa-spinner animate-spin"></i> <span>සකසමින්...</span>`;
            btn.disabled = true;

            showToast("Gemini AI විසින් සංගීතය විශ්ලේෂණය කරමින් පවතී...");

            const systemPrompt = "You are a professional electronic audio synthesizer architect. Your job is to return specialized musical parameters in JSON format representing the user's requested mood. Always return EXACTLY 8 bass notes frequencies, EXACTLY 8 high melody frequencies, a valid tempo between 60 and 150 BPM, and a 16-step binary drum sequence (kickPattern) that fits the rhythm perfectly.";
            
            const musicSchema = {
                type: "OBJECT",
                properties: {
                    title: { type: "STRING" },
                    artist: { type: "STRING" },
                    tempo: { type: "NUMBER" },
                    bassNotes: { 
                        type: "ARRAY", 
                        items: { type: "NUMBER" },
                        description: "Exactly 8 bass frequencies (e.g. 55, 65, 73, 82, 98, 110)"
                    },
                    melodyNotes: { 
                        type: "ARRAY", 
                        items: { type: "NUMBER" },
                        description: "Exactly 8 melody frequencies (e.g. 220, 261, 293, 329, 392, 440, 523)"
                    },
                    kickPattern: {
                        type: "ARRAY",
                        items: { type: "NUMBER" },
                        description: "Array of exactly 16 values of 0 or 1"
                    },
                    synthWaveType: { 
                        type: "STRING", 
                        description: "Only: 'sine', 'square', 'sawtooth', or 'triangle'" 
                    },
                    vibeDescription: { type: "STRING" }
                },
                required: ["title", "artist", "tempo", "bassNotes", "melodyNotes", "kickPattern", "synthWaveType", "vibeDescription"]
            };

            try {
                const response = await robustFetchGemini(
                    `Create synthesizer parameters for mood: "${moodInput}"`, 
                    systemPrompt, 
                    musicSchema
                );

                const dataText = response.candidates?.[0]?.content?.parts?.[0]?.text;
                if (!dataText) throw new Error("Incorrect payload response");

                const config = JSON.parse(dataText);
                synthesizeWavFromAiConfig(config);

            } catch (err) {
                showToast(err.message);
            } finally {
                btn.innerHTML = originalHtml;
                btn.disabled = false;
            }
        }

        // Synthesis from AI generated JSON schema
        function synthesizeWavFromAiConfig(config) {
            const sampleRate = 44100;
            const tempo = config.tempo || 110;
            const duration = 12; // 12 seconds
            const numSamples = sampleRate * duration;
            const audioBuffer = new Float32Array(numSamples);

            const bass = config.bassNotes || [110, 110, 130, 146, 110, 110, 165, 146];
            const melody = config.melodyNotes || [440, 440, 523, 587, 440, 440, 659, 587];
            const kickPattern = config.kickPattern || [1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0];
            const wave = config.synthWaveType || 'sine';

            for (let i = 0; i < numSamples; i++) {
                const t = i / sampleRate;
                const beatLen = 60 / tempo;
                const stepLen = beatLen / 4; // 16th notes
                const currentStep = Math.floor(t / stepLen) % 16;
                const currentBeat = Math.floor(t / beatLen);

                // Kick Drum Logic
                let kick = 0;
                if (kickPattern[currentStep] === 1) {
                    const stepTime = t % stepLen;
                    kick = Math.sin(2 * Math.PI * 60 * Math.exp(-stepTime * 12)) * Math.exp(-stepTime * 9);
                }

                // Synth Bass
                const bassIdx = currentBeat % bass.length;
                const bassFreq = bass[bassIdx];
                const bassTime = t % beatLen;
                const bassSignal = Math.sin(2 * Math.PI * bassFreq * t) * 0.22 * Math.exp(-bassTime * 4.5);

                // Synth Lead Melodies
                const melodyIdx = Math.floor(t / (beatLen / 2)) % melody.length;
                const melodyFreq = melody[melodyIdx];
                const melodyTime = t % (beatLen / 2);

                let leadSignal = 0;
                const phase = 2 * Math.PI * melodyFreq * t;
                if (wave === 'sine') leadSignal = Math.sin(phase);
                else if (wave === 'square') leadSignal = Math.sign(Math.sin(phase));
                else if (wave === 'sawtooth') leadSignal = (phase / Math.PI) % 2 - 1;
                else if (wave === 'triangle') leadSignal = Math.abs((phase / Math.PI) % 2 - 1) * 2 - 1;

                const lead = leadSignal * 0.09 * Math.exp(-melodyTime * 3.5);

                audioBuffer[i] = (kick * 0.6 + bassSignal + lead) * 0.35;
            }

            const binaryWav = createWavBinary(audioBuffer, sampleRate);
            const blob = new Blob([binaryWav], { type: 'audio/wav' });
            const url = URL.createObjectURL(blob);

            const aiTrack = {
                title: config.title || "AI Mood Melody",
                artist: config.artist || "Gemini Generator",
                url: url,
                cover: aestheticCovers[Math.floor(Math.random() * aestheticCovers.length)]
            };

            playlist.push(aiTrack);
            updatePlaylistUI();
            loadTrack(playlist.length - 1);
            playTrack();

            // Display AI commentary in UI
            const panel = document.getElementById('ai-response-panel');
            panel.classList.remove('hidden');
            document.getElementById('ai-response-title').textContent = `✨ AI Mood: ${config.title}`;
            document.getElementById('ai-response-content').textContent = `Vibe: ${config.vibeDescription}\n\nTempo: ${config.tempo} BPM\nWaveform: ${config.synthWaveType.toUpperCase()}`;
            
            showToast("AI BEAT SYNTHESIZED SUCCESSFULLY! ⚡");
        }

        // Feature 2: ✨ AI Lyricist & Meaning Generator
        async function generateSongLyricsAndMeaning() {
            if (currentTrackIndex === -1) {
                showToast("කරුණාකර පළමුව ගීතයක් වාදනය කරන්න!");
                return;
            }

            const currentTrack = playlist[currentTrackIndex];
            const panel = document.getElementById('ai-response-panel');
            const titleEl = document.getElementById('ai-response-title');
            const contentEl = document.getElementById('ai-response-content');

            panel.classList.remove('hidden');
            titleEl.textContent = `✨ ${currentTrack.title} සඳහා කාව්‍ය පද පේළි සකසමින්...`;
            contentEl.textContent = "Gemini AI මඟින් නිර්මාණාත්මක පද පේළි සහ ගීතයේ තේරුම ලියමින් පවතී. මොහොතක් රැඳෙන්න...";

            const systemPrompt = "You are a poetic songwriter who writes beautiful Sinhala music lyrics (with English translations) and explains the emotional meaning of songs based on titles. Always respond in beautiful Sinhala.";
            const userPrompt = `Write dynamic, soulful song lyrics in Sinhala and English, and explain the deep emotional meaning of a song titled "${currentTrack.title}" by "${currentTrack.artist}".`;

            try {
                const response = await robustFetchGemini(userPrompt, systemPrompt);
                const generatedText = response.candidates?.[0]?.content?.parts?.[0]?.text;

                if (!generatedText) throw new Error("Incorrect response payload.");

                titleEl.textContent = `✨ ${currentTrack.title} - පද සහ අර්ථය`;
                contentEl.textContent = generatedText;
                showToast("LYRICS GENERATED BY GEMINI AI!");

            } catch (err) {
                contentEl.textContent = err.message;
                showToast("පද රචනය අසාර්ථක විය.");
            }
        }

        function showToast(msg) {
            const t = document.getElementById('toast');
            const tm = document.getElementById('toast-msg');
            tm.textContent = msg;
            t.classList.remove('translate-y-24', 'opacity-0');
            t.classList.add('translate-y-0', 'opacity-100');
            setTimeout(() => {
                t.classList.remove('translate-y-0', 'opacity-100');
                t.classList.add('translate-y-24', 'opacity-0');
            }, 3000);
        }
    </script>
</body>
</html>
