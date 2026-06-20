<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>EcoTrack - Carbon Footprint Calculator</title>
    
    <style>
        /* Universal Styles */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            scroll-behavior: smooth;
        }

        body {
            background-color: #f4f7f5;
            color: #333;
        }

        /* Header */
        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 20px 8%;
            background-color: #ffffff;
            box-shadow: 0 4px 6px rgba(0,0,0,0.05);
            flex-wrap: wrap;
            gap: 15px;
        }

        .logo {
            font-size: 24px;
            font-weight: bold;
            color: #2e7d32;
        }

        .nav-controls {
            display: flex;
            align-items: center;
            gap: 20px;
            flex-wrap: wrap;
        }

        nav a {
            margin-left: 20px;
            text-decoration: none;
            color: #555;
            font-weight: 500;
        }

        nav a:hover {
            color: #2e7d32;
        }

        .lang-btn {
            background: #2e7d32;
            color: white;
            border: none;
            padding: 8px 18px;
            border-radius: 20px;
            font-weight: bold;
            cursor: pointer;
            transition: 0.3s;
            font-size: 14px;
        }

        .lang-btn:hover {
            background: #1b5e20;
            transform: translateY(-2px);
        }

        /* Hero Section */
        .hero {
            background: linear-gradient(rgba(46, 125, 50, 0.8), rgba(46, 125, 50, 0.9)), url('https://images.unsplash.com/photo-1542601906990-b4d3fb778b09?auto=format&fit=crop&w=1350&q=80') center/cover;
            color: white;
            text-align: center;
            padding: 100px 20px;
        }

        .hero h1 {
            font-size: 40px;
            margin-bottom: 20px;
        }

        .hero p {
            font-size: 18px;
            margin-bottom: 30px;
            max-width: 700px;
            margin-left: auto;
            margin-right: auto;
        }

        .btn {
            display: inline-block;
            padding: 12px 30px;
            background-color: #ffffff;
            color: #2e7d32;
            text-decoration: none;
            font-weight: bold;
            border-radius: 25px;
            transition: 0.3s;
        }

        .btn:hover {
            background-color: #e8f5e9;
            transform: translateY(-2px);
        }

        /* Calculator Container */
        .calc-container {
            max-width: 700px;
            margin: 60px auto;
            background: #ffffff;
            padding: 40px;
            border-radius: 12px;
            box-shadow: 0 10px 20px rgba(0,0,0,0.05);
        }

        .calc-container h2 {
            color: #2e7d32;
            margin-bottom: 10px;
        }

        .subtitle {
            color: #666;
            margin-bottom: 30px;
        }

        .form-group {
            margin-bottom: 25px;
        }

        .form-group label {
            display: block;
            margin-bottom: 10px;
            font-weight: 500;
        }

        .form-group select {
            width: 100%;
            padding: 12px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 16px;
            outline: none;
            transition: 0.3s;
        }

        .form-group select:focus {
            border-color: #2e7d32;
        }

        .btn-submit {
            width: 100%;
            padding: 15px;
            background-color: #2e7d32;
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 18px;
            font-weight: bold;
            cursor: pointer;
            transition: 0.3s;
        }

        .btn-submit:hover {
            background-color: #1b5e20;
        }

        /* Results Card */
        .result-card {
            margin-top: 40px;
            padding: 25px;
            border-radius: 8px;
            background-color: #e8f5e9;
            border-left: 6px solid #2e7d32;
            transition: all 0.5s ease;
        }

        .result-card h3 {
            margin-bottom: 10px;
        }

        .hidden {
            display: none;
        }

        .tips-section {
            margin-top: 20px;
            padding-top: 20px;
            border-top: 1px solid #c8e6c9;
        }

        .tips-section ul {
            margin-top: 10px;
            padding-left: 20px;
        }

        .tips-section li {
            margin-bottom: 8px;
        }

        footer {
            text-align: center;
            padding: 20px;
            background: #333;
            color: white;
            font-size: 14px;
            margin-top: 60px;
        }

        @media (max-width: 600px) {
            header {
                flex-direction: column;
                align-items: flex-start;
            }
            .nav-controls {
                width: 100%;
                justify-content: space-between;
            }
            nav a {
                margin-left: 0;
                margin-right: 15px;
            }
            .hero h1 {
                font-size: 28px;
            }
            .calc-container {
                padding: 20px;
                margin: 30px 15px;
            }
        }
    </style>
</head>
<body>

    <header>
        <div class="logo">🌿 EcoTrack</div>
        <div class="nav-controls">
            <nav>
                <a href="#calculator" data-key="nav-calculator">Calculator</a>
                <a href="#tips" data-key="nav-tips">Eco-Tips</a>
            </nav>
            <button class="lang-btn" id="langToggle" onclick="toggleLanguage()">🇮🇳 हिंदी</button>
        </div>
    </header>

    <section class="hero">
        <h1 data-key="hero-title">आपका लाइफस्टाइल पृथ्वी को कैसे प्रभावित कर रहा है?</h1>
        <p data-key="hero-desc">अपने रोज़मर्रा के कार्बन फुटप्रिंट को कैलकुलेट करें और पर्यावरण को बचाने में अपना योगदान दें।</p>
        <a href="#calculator" class="btn" data-key="hero-btn">अभी चेक करें</a>
    </section>

    <main id="calculator" class="calc-container">
        <h2 data-key="calc-title">Carbon Footprint Calculator</h2>
        <p class="subtitle" data-key="calc-subtitle">नीचे दिए गए आसान सवालों के जवाब दें:</p>

        <form id="footprintForm">
            <div class="form-group">
                <label for="transport" data-key="q1">1. आप रोज़ाना यात्रा (Travel) कैसे करते हैं?</label>
                <select id="transport" required>
                    <option value="0" data-key="opt-walk">पैदल या साइकिल (Zero Emissions)</option>
                    <option value="2" data-key="opt-public">पब्लिक ट्रांसपोर्ट (Bus/Metro)</option>
                    <option value="5" data-key="opt-two">टू-व्हीलर (Bike/Scooter)</option>
                    <option value="10" data-key="opt-four">फोर-व्हीलर (Car)</option>
                </select>
            </div>

            <div class="form-group">
                <label for="electricity" data-key="q2">2. आपके घर का मासिक बिजली बिल लगभग कितना आता है?</label>
                <select id="electricity" required>
                    <option value="2" data-key="opt-bill1">₹500 से कम</option>
                    <option value="5" data-key="opt-bill2">₹500 - ₹1500</option>
                    <option value="8" data-key="opt-bill3">₹1500 - ₹3000</option>
                    <option value="12" data-key="opt-bill4">₹3000 से ज़्यादा</option>
                </select>
            </div>

            <div class="form-group">
                <label for="diet" data-key="q3">3. आपकी डाइट (Diet) मुख्य रूप से कैसी है?</label>
                <select id="diet" required>
                    <option value="2" data-key="opt-veg">पूरी तरह शाकाहारी (Vegan/Vegetarian)</option>
                    <option value="6" data-key="opt-mixed">मिश्रित (कभी-कभी नॉन-वेज)</option>
                    <option value="10" data-key="opt-nonveg">नियमित मांसाहारी (Regular Non-Veg)</option>
                </select>
            </div>

            <div class="form-group">
                <label for="waste" data-key="q4">4. क्या आप अपने घर के कचरे को रीसायकल (Recycle) करते हैं?</label>
                <select id="waste" required>
                    <option value="1" data-key="opt-recycle-yes">हाँ, हमेशा</option>
                    <option value="3" data-key="opt-recycle-sometimes">कभी-कभी</option>
                    <option value="5" data-key="opt-recycle-no">नहीं, बिल्कुल नहीं</option>
                </select>
            </div>

            <button type="button" class="btn-submit" onclick="calculateScore()" data-key="calc-btn">Calculate My Score</button>
        </form>

        <div id="resultCard" class="result-card hidden">
            <h3 data-key="result-title">आपका कार्बन स्कोर: <span id="scoreValue">0</span> Points</h3>
            <p id="scoreAnalysis" data-key="result-analysis"></p>
            
            <div id="tips" class="tips-section">
                <h4 data-key="tips-title">🌿 आपके लिए खास ईको-टिप्स:</h4>
                <ul id="tipsList"></ul>
            </div>
        </div>
    </main>

    <footer>
        <p data-key="footer-text">© 2026 EcoTrack. पर्यावरण की सुरक्षा, हमारी ज़िम्मेदारी।</p>
    </footer>

    <script>
        // ===== Bilingual Data =====
        const translations = {
            en: {
                // Header
                "nav-calculator": "Calculator",
                "nav-tips": "Eco-Tips",
                // Hero
                "hero-title": "How does your lifestyle impact the Earth?",
                "hero-desc": "Calculate your daily carbon footprint and contribute to saving the environment.",
                "hero-btn": "Check Now",
                // Calculator
                "calc-title": "Carbon Footprint Calculator",
                "calc-subtitle": "Answer the simple questions below:",
                "q1": "1. How do you travel daily?",
                "q2": "2. What is your monthly electricity bill approximately?",
                "q3": "3. What is your diet primarily?",
                "q4": "4. Do you recycle your household waste?",
                "calc-btn": "Calculate My Score",
                // Options
                "opt-walk": "Walking or Cycling (Zero Emissions)",
                "opt-public": "Public Transport (Bus/Metro)",
                "opt-two": "Two-Wheeler (Bike/Scooter)",
                "opt-four": "Four-Wheeler (Car)",
                "opt-bill1": "Less than ₹500",
                "opt-bill2": "₹500 - ₹1500",
                "opt-bill3": "₹1500 - ₹3000",
                "opt-bill4": "More than ₹3000",
                "opt-veg": "Fully Vegetarian (Vegan/Vegetarian)",
                "opt-mixed": "Mixed (Sometimes Non-Veg)",
                "opt-nonveg": "Regular Non-Veg",
                "opt-recycle-yes": "Yes, always",
                "opt-recycle-sometimes": "Sometimes",
                "opt-recycle-no": "No, not at all",
                // Results
                "result-title": "Your Carbon Score: ",
                "result-analysis": "",
                "tips-title": "🌿 Special Eco-Tips for You:",
                // Footer
                "footer-text": "© 2026 EcoTrack. Protecting the environment is our responsibility."
            },
            hi: {
                // Header
                "nav-calculator": "कैलकुलेटर",
                "nav-tips": "ईको-टिप्स",
                // Hero
                "hero-title": "आपका लाइफस्टाइल पृथ्वी को कैसे प्रभावित कर रहा है?",
                "hero-desc": "अपने रोज़मर्रा के कार्बन फुटप्रिंट को कैलकुलेट करें और पर्यावरण को बचाने में अपना योगदान दें।",
                "hero-btn": "अभी चेक करें",
                // Calculator
                "calc-title": "कार्बन फुटप्रिंट कैलकुलेटर",
                "calc-subtitle": "नीचे दिए गए आसान सवालों के जवाब दें:",
                "q1": "1. आप रोज़ाना यात्रा (Travel) कैसे करते हैं?",
                "q2": "2. आपके घर का मासिक बिजली बिल लगभग कितना आता है?",
                "q3": "3. आपकी डाइट (Diet) मुख्य रूप से कैसी है?",
                "q4": "4. क्या आप अपने घर के कचरे को रीसायकल (Recycle) करते हैं?",
                "calc-btn": "मेरा स्कोर कैलकुलेट करें",
                // Options
                "opt-walk": "पैदल या साइकिल (Zero Emissions)",
                "opt-public": "पब्लिक ट्रांसपोर्ट (Bus/Metro)",
                "opt-two": "टू-व्हीलर (Bike/Scooter)",
                "opt-four": "फोर-व्हीलर (Car)",
                "opt-bill1": "₹500 से कम",
                "opt-bill2": "₹500 - ₹1500",
                "opt-bill3": "₹1500 - ₹3000",
                "opt-bill4": "₹3000 से ज़्यादा",
                "opt-veg": "पूरी तरह शाकाहारी (Vegan/Vegetarian)",
                "opt-mixed": "मिश्रित (कभी-कभी नॉन-वेज)",
                "opt-nonveg": "नियमित मांसाहारी (Regular Non-Veg)",
                "opt-recycle-yes": "हाँ, हमेशा",
                "opt-recycle-sometimes": "कभी-कभी",
                "opt-recycle-no": "नहीं, बिल्कुल नहीं",
                // Results
                "result-title": "आपका कार्बन स्कोर: ",
                "result-analysis": "",
                "tips-title": "🌿 आपके लिए खास ईको-टिप्स:",
                // Footer
                "footer-text": "© 2026 EcoTrack. पर्यावरण की सुरक्षा, हमारी ज़िम्मेदारी।"
            }
        };

        let currentLang = 'hi'; // Default Hindi

        // ===== Toggle Language =====
        function toggleLanguage() {
            currentLang = (currentLang === 'hi') ? 'en' : 'hi';
            updateLanguage();
            // Update button text
            const btn = document.getElementById('langToggle');
            btn.textContent = (currentLang === 'hi') ? '🇬🇧 English' : '🇮🇳 हिंदी';
        }

        function updateLanguage() {
            const langData = translations[currentLang];
            // Update all elements with data-key attribute
            document.querySelectorAll('[data-key]').forEach(el => {
                const key = el.getAttribute('data-key');
                if (langData[key] !== undefined) {
                    // For elements with innerHTML (like hero title, etc.)
                    if (el.tagName === 'H1' || el.tagName === 'P' || el.tagName === 'A' || 
                        el.tagName === 'H2' || el.tagName === 'H3' || el.tagName === 'H4' ||
                        el.tagName === 'LABEL' || el.tagName === 'BUTTON') {
                        el.innerHTML = langData[key];
                    } else {
                        el.textContent = langData[key];
                    }
                }
            });

            // Update all select options
            document.querySelectorAll('select option').forEach(opt => {
                const key = opt.getAttribute('data-key');
                if (key && langData[key] !== undefined) {
                    opt.textContent = langData[key];
                }
            });

            // Update placeholder text if any
            // Also update the result analysis if it's already showing
            const scoreAnalysis = document.getElementById('scoreAnalysis');
            if (!scoreAnalysis.classList.contains('hidden') && scoreAnalysis.innerHTML !== '') {
                // Re-run analysis with current language context
                const totalScore = parseInt(document.getElementById('scoreValue').innerText);
                updateResultAnalysis(totalScore);
            }
        }

        // ===== Result Analysis with Language Support =====
        function updateResultAnalysis(score) {
            const analysisEl = document.getElementById('scoreAnalysis');
            const tipsList = document.getElementById('tipsList');
            
            if (score <= 10) {
                analysisEl.innerHTML = currentLang === 'hi' 
                    ? "🌱 <b>शानदार!</b> आपका कार्बन फुटप्रिंट बहुत कम है। आप पर्यावरण के सच्चे मित्र हैं!"
                    : "🌱 <b>Excellent!</b> Your carbon footprint is very low. You are a true friend of the environment!";
                tipsList.innerHTML = currentLang === 'hi'
                    ? "<li>इसी तरह अपनी अच्छी आदतें बनाए रखें।</li><li>दूसरों को भी जागरूक करें।</li>"
                    : "<li>Keep up your good habits.</li><li>Inspire others to do the same.</li>";
            } 
            else if (score > 10 && score <= 22) {
                analysisEl.innerHTML = currentLang === 'hi'
                    ? "⚠️ <b>औसत (Average):</b> आपका स्कोर ठीक है, लेकिन इसमें और सुधार की गुंजाइश है।"
                    : "⚠️ <b>Average:</b> Your score is decent, but there's room for improvement.";
                // Dynamic tips
                generateDynamicTips(score, tipsList);
            } 
            else {
                analysisEl.innerHTML = currentLang === 'hi'
                    ? "🚨 <b>हाई अलर्ट!</b> आपका कार्बन फुटप्रिंट काफी ज़्यादा है। पृथ्वी को बचाने के लिए आपको तुरंत बदलाव करने होंगे।"
                    : "🚨 <b>High Alert!</b> Your carbon footprint is too high. You need to make immediate changes to save the Earth.";
                generateDynamicTips(score, tipsList);
            }
        }

        function generateDynamicTips(score, list) {
            // Clear previous tips
            list.innerHTML = '';
            const tips = [];
            
            // Transport tips
            const transportVal = parseInt(document.getElementById('transport').value);
            if (transportVal >= 5) {
                tips.push(currentLang === 'hi' 
                    ? "हफ़्ते में कम से कम 2 दिन कार/बाइक की जगह पब्लिक ट्रांसपोर्ट या साइकिल का यूज़ करें।"
                    : "Use public transport or cycle at least 2 days a week instead of car/bike.");
            }
            
            // Electricity tips
            const elecVal = parseInt(document.getElementById('electricity').value);
            if (elecVal >= 8) {
                tips.push(currentLang === 'hi'
                    ? "घर के अप्लायंसेज को बंद करना न भूलें और LED बल्ब का इस्तेमाल बढ़ाएं।"
                    : "Don't forget to turn off appliances and switch to LED bulbs.");
            }
            
            // Diet tips
            const dietVal = parseInt(document.getElementById('diet').value);
            if (dietVal >= 6) {
                tips.push(currentLang === 'hi'
                    ? "अपनी डाइट में प्लांट-बेस्ड (शाकाहारी) भोजन को थोड़ा और शामिल करें।"
                    : "Try to include more plant-based meals in your diet.");
            }
            
            // Waste tips
            const wasteVal = parseInt(document.getElementById('waste').value);
            if (wasteVal >= 3) {
                tips.push(currentLang === 'hi'
                    ? "घर के सूखे और गीले कचरे को अलग करें और रीसायकल करने की आदत डालें।"
                    : "Separate dry and wet waste and develop a habit of recycling.");
            }
            
            // If no specific tips, add general ones
            if (tips.length === 0) {
                tips.push(currentLang === 'hi'
                    ? "आप पहले से ही बहुत अच्छा कर रहे हैं! इन आदतों को बनाए रखें।"
                    : "You're already doing great! Keep up these habits.");
            }
            
            tips.forEach(tip => {
                const li = document.createElement('li');
                li.textContent = tip;
                list.appendChild(li);
            });
        }

        // ===== Main Calculate Function =====
        function calculateScore() {
            const transport = parseInt(document.getElementById('transport').value);
            const electricity = parseInt(document.getElementById('electricity').value);
            const diet = parseInt(document.getElementById('diet').value);
            const waste = parseInt(document.getElementById('waste').value);

            const totalScore = transport + electricity + diet + waste;

            const resultCard = document.getElementById('resultCard');
            resultCard.classList.remove('hidden');

            document.getElementById('scoreValue').innerText = totalScore;

            // Update analysis based on score
            updateResultAnalysis(totalScore);

            // Color coding based on score
            if (totalScore <= 10) {
                resultCard.style.borderColor = "#2e7d32";
                resultCard.style.backgroundColor = "#e8f5e9";
            } 
            else if (totalScore > 10 && totalScore <= 22) {
                resultCard.style.borderColor = "#fbc02d";
                resultCard.style.backgroundColor = "#fffde7";
            } 
            else {
                resultCard.style.borderColor = "#d32f2f";
                resultCard.style.backgroundColor = "#ffebee";
            }

            resultCard.scrollIntoView({ behavior: 'smooth' });
        }

        // ===== Initial language setup =====
        document.addEventListener('DOMContentLoaded', function() {
            // Set default language to Hindi as per original design
            currentLang = 'hi';
            updateLanguage();
            document.getElementById('langToggle').textContent = '🇬🇧 English';
        });
    </script>
</body>
</html>
