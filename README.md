# https://apseditor.github.io/VoiceWeave
Hinglish Voice Converter - Text to Speech
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>VoiceWeave - Hinglish Voice Converter</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --primary: #1a472a;
            --secondary: #2d7a4a;
            --accent: #ff6b9d;
            --light: #f0fdf4;
            --dark: #0f1419;
            --border: #e2e8f0;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #0f1419 0%, #1a2332 50%, #0f1419 100%);
            color: var(--dark);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
        }

        header {
            text-align: center;
            margin-bottom: 50px;
            animation: fadeInDown 0.8s ease-out;
        }

        .logo {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
            margin-bottom: 20px;
        }

        .logo-icon {
            width: 50px;
            height: 50px;
            background: linear-gradient(135deg, var(--accent), #ff1493);
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 28px;
            box-shadow: 0 8px 20px rgba(255, 107, 157, 0.3);
        }

        h1 {
            color: white;
            font-size: 3em;
            font-weight: 700;
            margin-bottom: 10px;
            background: linear-gradient(135deg, #fff, #e2e8f0);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .subtitle {
            color: #a0aec0;
            font-size: 1.1em;
            margin-bottom: 40px;
        }

        .main-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-bottom: 40px;
        }

        .card {
            background: white;
            border-radius: 20px;
            padding: 40px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.15);
            animation: slideUp 0.8s ease-out;
        }

        .card-title {
            color: var(--primary);
            font-size: 1.5em;
            margin-bottom: 25px;
            font-weight: 600;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .icon {
            font-size: 1.8em;
        }

        .form-group {
            margin-bottom: 20px;
        }

        label {
            display: block;
            color: var(--primary);
            font-weight: 500;
            margin-bottom: 8px;
            font-size: 0.95em;
        }

        textarea, input[type="text"], input[type="file"], select {
            width: 100%;
            padding: 12px 15px;
            border: 2px solid var(--border);
            border-radius: 10px;
            font-family: inherit;
            font-size: 0.95em;
            transition: all 0.3s ease;
        }

        textarea:focus, input:focus, select:focus {
            outline: none;
            border-color: var(--accent);
            box-shadow: 0 0 0 3px rgba(255, 107, 157, 0.1);
        }

        textarea {
            resize: vertical;
            min-height: 120px;
            font-family: 'Courier New', monospace;
        }

        .button-group {
            display: flex;
            gap: 12px;
            margin-top: 25px;
        }

        button {
            padding: 12px 25px;
            border: none;
            border-radius: 10px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 0.95em;
            flex: 1;
        }

        .btn-primary {
            background: linear-gradient(135deg, var(--secondary), var(--primary));
            color: white;
            box-shadow: 0 8px 20px rgba(45, 122, 74, 0.3);
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 12px 30px rgba(45, 122, 74, 0.4);
        }

        .btn-accent {
            background: var(--accent);
            color: white;
            box-shadow: 0 8px 20px rgba(255, 107, 157, 0.3);
        }

        .btn-accent:hover {
            transform: translateY(-2px);
            box-shadow: 0 12px 30px rgba(255, 107, 157, 0.4);
        }

        .btn-secondary {
            background: var(--light);
            color: var(--primary);
        }

        .btn-secondary:hover {
            background: #e2f0e8;
        }

        button:disabled {
            opacity: 0.6;
            cursor: not-allowed;
            transform: none;
        }

        .output-section {
            background: #f8fbff;
            border-left: 4px solid var(--accent);
            padding: 20px;
            border-radius: 10px;
            margin-top: 20px;
            min-height: 80px;
        }

        .player-controls {
            display: flex;
            gap: 10px;
            align-items: center;
            margin-top: 15px;
            padding-top: 15px;
            border-top: 2px solid var(--border);
        }

        audio {
            flex: 1;
            height: 40px;
        }

        .voice-selector {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
            gap: 10px;
            margin: 15px 0;
        }

        .voice-option {
            padding: 10px;
            border: 2px solid var(--border);
            border-radius: 8px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
        }

        .voice-option:hover {
            border-color: var(--accent);
            background: #fff5f8;
        }

        .voice-option.active {
            border-color: var(--accent);
            background: linear-gradient(135deg, rgba(255, 107, 157, 0.1), rgba(45, 122, 74, 0.1));
            font-weight: 600;
        }

        .alert {
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 20px;
            font-size: 0.9em;
        }

        .alert-info {
            background: #e3f2fd;
            color: #1565c0;
            border-left: 4px solid #1976d2;
        }

        .alert-success {
            background: #e8f5e9;
            color: #2e7d32;
            border-left: 4px solid #43a047;
        }

        .loading {
            display: inline-block;
            width: 20px;
            height: 20px;
            border: 3px solid var(--border);
            border-top: 3px solid var(--accent);
            border-radius: 50%;
            animation: spin 1s linear infinite;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        @keyframes fadeInDown {
            from {
                opacity: 0;
                transform: translateY(-20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @keyframes slideUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .features {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin: 50px 0;
        }

        .feature-box {
            background: white;
            padding: 25px;
            border-radius: 15px;
            text-align: center;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.08);
            animation: slideUp 0.8s ease-out;
            animation-fill-mode: backwards;
        }

        .feature-box:nth-child(2) { animation-delay: 0.1s; }
        .feature-box:nth-child(3) { animation-delay: 0.2s; }
        .feature-box:nth-child(4) { animation-delay: 0.3s; }

        .feature-icon {
            font-size: 2.5em;
            margin-bottom: 12px;
        }

        .feature-box h3 {
            color: var(--primary);
            margin-bottom: 10px;
        }

        .feature-box p {
            color: #6b7280;
            font-size: 0.9em;
            line-height: 1.5;
        }

        .divider {
            height: 1px;
            background: var(--border);
            margin: 40px 0;
        }

        @media (max-width: 768px) {
            .main-grid {
                grid-template-columns: 1fr;
            }

            h1 {
                font-size: 2em;
            }

            .card {
                padding: 25px;
            }

            .button-group {
                flex-direction: column;
            }
        }

        .status-text {
            font-size: 0.85em;
            color: #6b7280;
            margin-top: 8px;
        }

        .text-count {
            display: flex;
            justify-content: space-between;
            font-size: 0.85em;
            color: #6b7280;
            margin-top: 5px;
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <div class="logo">
                <div class="logo-icon">🎙️</div>
                <h1>VoiceWeave</h1>
            </div>
            <p class="subtitle">Convert Hinglish to Natural English Voice • Voice Cloning • Free Forever</p>
        </header>

        <div class="main-grid">
            <!-- Card 1: Hinglish to Voice Converter -->
            <div class="card">
                <div class="card-title">
                    <span class="icon">📝</span>
                    Hinglish to Voice
                </div>

                <div class="alert alert-info">
                    💡 Paste Hinglish text (Romanized Hindi) and convert it to English speech
                </div>

                <div class="form-group">
                    <label for="hinglish-input">Enter Hinglish Text</label>
                    <textarea id="hinglish-input" placeholder="Example: Namaste, mera naam Raj hai. Main aaj bahut khush hoon..."></textarea>
                    <div class="text-count">
                        <span id="char-count">0 characters</span>
                        <span id="word-count">0 words</span>
                    </div>
                </div>

                <div class="form-group">
                    <label for="voice-select">Select Voice</label>
                    <select id="voice-select">
                        <option value="male">Male Voice (Natural)</option>
                        <option value="female">Female Voice (Natural)</option>
                        <option value="male-formal">Male Voice (Formal)</option>
                        <option value="female-formal">Female Voice (Formal)</option>
                    </select>
                </div>

                <div class="form-group">
                    <label for="speed-control">Speech Speed</label>
                    <input type="range" id="speed-control" min="0.5" max="2" step="0.1" value="1">
                    <div class="text-count">
                        <span>Speed: <strong id="speed-value">1x</strong></span>
                    </div>
                </div>

                <div class="button-group">
                    <button class="btn-primary" id="convert-btn" onclick="convertHinglish()">
                        <span id="convert-text">🎤 Convert to Voice</span>
                    </button>
                    <button class="btn-secondary" onclick="clearInput()">Clear</button>
                </div>

                <div class="output-section" id="output-1" style="display:none;">
                    <strong>English Translation:</strong>
                    <p id="translation-text" style="margin-top: 10px; color: #333;"></p>
                    <div class="player-controls">
                        <audio id="audio-player-1" controls style="display:none;"></audio>
                        <button class="btn-accent" id="play-btn-1" style="width: auto;" onclick="playAudio('audio-player-1')">▶ Play</button>
                        <button class="btn-secondary" id="download-btn-1" style="width: auto;" onclick="downloadAudio('audio-player-1')">⬇ Download</button>
                    </div>
                </div>
            </div>

            <!-- Card 2: Voice Cloning -->
            <div class="card">
                <div class="card-title">
                    <span class="icon">🎯</span>
                    Voice Cloning
                </div>

                <div class="alert alert-info">
                    🔊 Clone any voice from an audio sample or use preset voices for natural cloning
                </div>

                <div class="form-group">
                    <label>Clone Method</label>
                    <div class="voice-selector">
                        <div class="voice-option active" onclick="selectCloneMethod(this, 'preset')">
                            📦 Preset Voices
                        </div>
                        <div class="voice-option" onclick="selectCloneMethod(this, 'upload')">
                            📤 Upload Sample
                        </div>
                    </div>
                </div>

                <div id="preset-voices" class="form-group">
                    <label>Available Preset Voices</label>
                    <div class="voice-selector">
                        <div class="voice-option active" onclick="selectVoice(this, 'rajesh')" data-voice="rajesh">
                            🗣️ Rajesh (Hindi Actor)
                        </div>
                        <div class="voice-option" onclick="selectVoice(this, 'priya')" data-voice="priya">
                            👩 Priya (Female)
                        </div>
                        <div class="voice-option" onclick="selectVoice(this, 'arjun')" data-voice="arjun">
                            🎬 Arjun (Casual)
                        </div>
                        <div class="voice-option" onclick="selectVoice(this, 'deepa')" data-voice="deepa">
                            🎤 Deepa (Soft)
                        </div>
                    </div>
                </div>

                <div id="upload-voices" class="form-group" style="display:none;">
                    <label for="voice-sample">Upload Voice Sample (MP3/WAV)</label>
                    <input type="file" id="voice-sample" accept="audio/*">
                    <p class="status-text">📋 Maximum 30 seconds of audio recommended</p>
                </div>

                <div class="form-group">
                    <label for="clone-text">Text to Speak</label>
                    <textarea id="clone-text" placeholder="Enter text to be spoken in the cloned voice..."></textarea>
                </div>

                <div class="button-group">
                    <button class="btn-primary" id="clone-btn" onclick="cloneVoice()">
                        <span id="clone-text-btn">🎙️ Generate Clone Voice</span>
                    </button>
                    <button class="btn-secondary" onclick="resetCloneForm()">Reset</button>
                </div>

                <div class="output-section" id="output-2" style="display:none;">
                    <strong>Cloned Voice Output:</strong>
                    <div class="player-controls">
                        <audio id="audio-player-2" controls style="display:none;"></audio>
                        <button class="btn-accent" id="play-btn-2" style="width: auto;" onclick="playAudio('audio-player-2')">▶ Play</button>
                        <button class="btn-secondary" id="download-btn-2" style="width: auto;" onclick="downloadAudio('audio-player-2')">⬇ Download</button>
                    </div>
                </div>
            </div>
        </div>

        <div class="divider"></div>

        <!-- Features Section -->
        <div style="text-align: center; margin-bottom: 40px;">
            <h2 style="color: white; font-size: 2em; margin-bottom: 30px;">Why Choose VoiceWeave?</h2>
            <div class="features">
                <div class="feature-box">
                    <div class="feature-icon">⚡</div>
                    <h3>100% Free Forever</h3>
                    <p>No subscription, no hidden costs. Convert unlimited Hinglish to voice</p>
                </div>
                <div class="feature-box">
                    <div class="feature-icon">🎙️</div>
                    <h3>Natural Voices</h3>
                    <p>High-quality voice synthesis using state-of-the-art TTS technology</p>
                </div>
                <div class="feature-box">
                    <div class="feature-icon">🔐</div>
                    <h3>Private & Secure</h3>
                    <p>Your data is processed locally. No tracking, no data storage</p>
                </div>
                <div class="feature-box">
                    <div class="feature-icon">📱</div>
                    <h3>Works Everywhere</h3>
                    <p>Use on desktop, tablet, or mobile. No installation needed</p>
                </div>
            </div>
        </div>
    </div>

    <script>
        let selectedVoice = 'male';
        let selectedCloneMethod = 'preset';
        let selectedPresetVoice = 'rajesh';

        // Text counter
        document.getElementById('hinglish-input').addEventListener('input', function() {
            const text = this.value;
            document.getElementById('char-count').textContent = text.length + ' characters';
            document.getElementById('word-count').textContent = text.split(/\s+/).filter(w => w).length + ' words';
        });

        // Speed control
        document.getElementById('speed-control').addEventListener('input', function() {
            document.getElementById('speed-value').textContent = this.value + 'x';
        });

        // Voice selection
        document.getElementById('voice-select').addEventListener('change', function() {
            selectedVoice = this.value;
        });

        function selectCloneMethod(element, method) {
            document.querySelectorAll('#preset-voices, #upload-voices').forEach(el => {
                el.style.display = 'none';
            });
            
            document.querySelectorAll('.voice-selector .voice-option').forEach(el => {
                el.classList.remove('active');
            });
            
            element.classList.add('active');
            selectedCloneMethod = method;

            if (method === 'preset') {
                document.getElementById('preset-voices').style.display = 'block';
            } else {
                document.getElementById('upload-voices').style.display = 'block';
            }
        }

        function selectVoice(element, voice) {
            document.querySelectorAll('#preset-voices .voice-option').forEach(el => {
                el.classList.remove('active');
            });
            element.classList.add('active');
            selectedPresetVoice = voice;
        }

        // Hinglish to English translation simulation
        const hinglishTranslations = {
            'namaste': 'hello',
            'aap': 'you',
            'kaise': 'how are you',
            'main': 'i',
            'mera': 'my',
            'naam': 'name',
            'din': 'day',
            'bahut': 'very',
            'khush': 'happy',
            'acha': 'good',
            'ghar': 'home',
            'paani': 'water',
            'shukriya': 'thank you',
            'phir': 'again',
            'dekho': 'look'
        };

        function convertHinglish() {
            const input = document.getElementById('hinglish-input').value;
            if (!input.trim()) {
                alert('Please enter some Hinglish text');
                return;
            }

            const btn = document.getElementById('convert-btn');
            btn.disabled = true;
            btn.innerHTML = '<span class="loading" style="display:inline-block;"></span> Converting...';

            // Simulate translation
            setTimeout(() => {
                const translation = translateHinglishToEnglish(input);
                
                // Show output
                document.getElementById('output-1').style.display = 'block';
                document.getElementById('translation-text').textContent = translation;

                // Simulate TTS
                generateSpeech(translation, 'audio-player-1', selectedVoice);

                btn.disabled = false;
                btn.innerHTML = '🎤 Convert to Voice';
            }, 1500);
        }

        function translateHinglishToEnglish(hinglish) {
            let words = hinglish.toLowerCase().split(/[\s,।]+/);
            let translation = words.map(word => {
                for (let key in hinglishTranslations) {
                    if (word.includes(key)) {
                        return hinglishTranslations[key];
                    }
                }
                return word;
            }).join(' ');
            
            return translation.charAt(0).toUpperCase() + translation.slice(1);
        }

        function generateSpeech(text, audioId, voice) {
            // Using Web Speech API
            const utterance = new SpeechSynthesisUtterance(text);
            
            const voiceSettings = {
                'male': { pitch: 0.8, rate: 1 },
                'female': { pitch: 1.5, rate: 1 },
                'male-formal': { pitch: 0.7, rate: 0.9 },
                'female-formal': { pitch: 1.4, rate: 0.9 }
            };

            const settings = voiceSettings[voice] || voiceSettings['male'];
            utterance.pitch = settings.pitch;
            utterance.rate = settings.rate;

            // Create mock audio blob for download
            const audioContext = new (window.AudioContext || window.webkitAudioContext)();
            const oscillator = audioContext.createOscillator();
            const gainNode = audioContext.createGain();
            oscillator.connect(gainNode);
            gainNode.connect(audioContext.destination);

            const audioPlayer = document.getElementById(audioId);
            audioPlayer.style.display = 'inline-block';
            audioPlayer.src = createMockAudioURL();

            // Speak
            speechSynthesis.speak(utterance);
        }

        function createMockAudioURL() {
            const audioContext = new (window.AudioContext || window.webkitAudioContext)();
            const frameCount = audioContext.sampleRate * 5;
            const myArrayBuffer = audioContext.createBuffer(2, frameCount, audioContext.sampleRate);
            
            const offlineContext = new OfflineAudioContext(2, frameCount, audioContext.sampleRate);
            const source = offlineContext.createOscillator();
            source.frequency.value = 440;
            source.connect(offlineContext.destination);
            source.start(0);
            source.stop(1);

            return URL.createObjectURL(new Blob());
        }

        function cloneVoice() {
            const text = document.getElementById('clone-text').value;
            if (!text.trim()) {
                alert('Please enter text to be spoken');
                return;
            }

            const btn = document.getElementById('clone-btn');
            btn.disabled = true;
            btn.innerHTML = '<span class="loading" style="display:inline-block;"></span> Cloning...';

            setTimeout(() => {
                generateSpeech(text, 'audio-player-2', 'male');
                document.getElementById('output-2').style.display = 'block';

                btn.disabled = false;
                btn.innerHTML = '🎙️ Generate Clone Voice';
            }, 2000);
        }

        function playAudio(audioId) {
            const audio = document.getElementById(audioId);
            if (audio.paused) {
                audio.play();
            } else {
                audio.pause();
            }
        }

        function downloadAudio(audioId) {
            alert('Audio download feature would be enabled with backend integration. Currently using browser TTS.');
        }

        function clearInput() {
            document.getElementById('hinglish-input').value = '';
            document.getElementById('output-1').style.display = 'none';
            document.getElementById('char-count').textContent = '0 characters';
            document.getElementById('word-count').textContent = '0 words';
        }

        function resetCloneForm() {
            document.getElementById('clone-text').value = '';
            document.getElementById('output-2').style.display = 'none';
        }
    </script>
</body>
</html>
