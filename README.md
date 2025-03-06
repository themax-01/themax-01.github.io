# themax-01.github.io
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Special Birthday Card</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            font-family: 'Arial', sans-serif;
            overflow: hidden;
            transition: background 8s ease;
            background: linear-gradient(to bottom, #f8e1eb, #ffd1dc);
        }
        
        .card {
            position: relative;
            width: 80%;
            max-width: 500px;
            background-color: rgba(255, 255, 255, 0.85);
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            padding: 30px;
            text-align: center;
            animation: float 6s ease-in-out infinite;
            z-index: 10;
            transition: all 8s ease;
            overflow: hidden;
        }
        
        @keyframes float {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-20px); }
        }
        
        h1 {
            margin-bottom: 10px;
            font-size: 32px;
            transition: color 8s ease, text-shadow 8s ease;
            color: #e87a90;
        }
        
        .highlight {
            font-weight: bold;
            transition: color 8s ease;
            color: #d25380;
        }
        
        .falling {
            position: absolute;
            pointer-events: none;
            z-index: 1;
            animation: fall linear infinite;
        }
        
        @keyframes fall {
            0% {
                transform: translateY(-5vh) rotate(0deg);
                opacity: 0;
            }
            10% {
                opacity: 1;
            }
            90% {
                opacity: 0.8;
            }
            100% {
                transform: translateY(105vh) rotate(360deg);
                opacity: 0;
            }
        }
        
        .heart-container {
            position: relative;
            width: 200px;
            height: 180px;
            margin: 10px auto 20px;
            transition: all 8s ease;
        }
        
        .heart {
            background-color: #e74c3c;
            height: 150px;
            width: 150px;
            transform: rotate(-45deg);
            position: relative;
            margin: auto;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.15);
            transition: all 8s ease;
            animation: pulse 1.5s ease-in-out infinite;
        }
        
        .heart:before, .heart:after {
            content: "";
            background-color: #e74c3c;
            border-radius: 50%;
            height: 150px;
            position: absolute;
            width: 150px;
            transition: all 8s ease;
        }
        
        .heart:before {
            top: -75px;
            left: 0;
        }
        
        .heart:after {
            left: 75px;
            top: 0;
        }
        
        @keyframes pulse {
            0% { transform: rotate(-45deg) scale(1); }
            50% { transform: rotate(-45deg) scale(1.1); }
            100% { transform: rotate(-45deg) scale(1); }
        }
        
        .quote-container {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 80%;
            text-align: center;
            color: white;
            font-size: 14px;
            font-weight: bold;
            text-shadow: 0 1px 3px rgba(0, 0, 0, 0.3);
            opacity: 0;
            animation: fadeInOut 10s linear infinite;
            z-index: 2;
        }
        
        @keyframes fadeInOut {
            0%, 100% { opacity: 0; }
            15%, 85% { opacity: 1; }
        }
        
        .doodle {
            position: absolute;
            width: 70px;
            height: 70px;
            opacity: 0.7;
            transition: all 8s ease;
        }
        
        .doodle1 {
            top: 20px;
            left: 20px;
            transform: rotate(-15deg);
        }
        
        .doodle2 {
            bottom: 20px;
            right: 20px;
            transform: rotate(10deg);
        }
        
        .doodle3 {
            bottom: 30px;
            left: 25px;
            transform: rotate(-5deg);
        }
        
        .doodle4 {
            top: 30px;
            right: 25px;
            transform: rotate(20deg);
        }
        
        .date {
            font-size: 18px;
            margin-top: 10px;
            margin-bottom: 20px;
            transition: color 8s ease;
        }
    </style>
</head>
<body>
    <div class="card">
        <h1>Happy Birthday!</h1>
        <div class="date">March 27th</div>
        
        <div class="heart-container">
            <div class="heart"></div>
            <div class="quote-container" id="quote-display"></div>
        </div>
        
        <!-- Doodles - will be replaced with theme-specific elements -->
        <div class="doodle doodle1" id="doodle1"></div>
        <div class="doodle doodle2" id="doodle2"></div>
        <div class="doodle doodle3" id="doodle3"></div>
        <div class="doodle doodle4" id="doodle4"></div>
    </div>
    
    <script>
        // Define theme configurations
        const themes = {
            theme1: {
                name: "Cherry Blossom",
                background: "linear-gradient(to bottom, #f8e1eb, #ffd1dc)",
                cardBg: "rgba(255, 255, 255, 0.85)",
                textColor: "#e87a90",
                highlightColor: "#d25380",
                heartColor: "#e87a90",
                heartShadow: "0 5px 15px rgba(232, 122, 144, 0.5)",
                fallingItems: ["petal", 80, ["#ffd7e9", "#ffc2d1", "#ffb6c1", "#f8bbd0"]],
                doodles: ["🌸", "🌿", "🦋", "☁️"]
            },
            theme2: {
                name: "Love",
                background: "linear-gradient(to bottom, #ff5e79, #ff1a40)",
                cardBg: "rgba(255, 255, 255, 0.85)",
                textColor: "#e60026",
                highlightColor: "#ff2251",
                heartColor: "#ff0033",
                heartShadow: "0 5px 15px rgba(255, 0, 51, 0.5)",
                fallingItems: ["heart", 70, ["#ff0033", "#ff3366", "#ff6699", "#ffffff"]],
                doodles: ["💘", "💌", "💖", "💕"]
            },
            theme3: {
                name: "Neon",
                background: "linear-gradient(45deg, #000000, #0f0f0f, #1a1a1a)",
                cardBg: "rgba(20, 20, 20, 0.8)",
                textColor: "#00ffbb",
                highlightColor: "#00eeff",
                heartColor: "#00ff99",
                heartShadow: "0 5px 15px rgba(0, 255, 153, 0.7), 0 0 30px rgba(0, 255, 153, 0.5)",
                fallingItems: ["neon", 60, ["#00ff00", "#ff00ff", "#00ffff", "#ffff00"]],
                doodles: ["🎧", "🎵", "🎮", "✨"]
            },
            theme4: {
                name: "Spring",
                background: "linear-gradient(to bottom, #a7d84e, #52b788)",
                cardBg: "rgba(255, 255, 255, 0.85)",
                textColor: "#2d6a4f",
                highlightColor: "#52b788",
                heartColor: "#52b788",
                heartShadow: "0 5px 15px rgba(82, 183, 136, 0.5)",
                fallingItems: ["flower", 65, ["#ffec99", "#a7d84e", "#f4acb7", "#ffffff"]],
                doodles: ["🌱", "🌷", "🌼", "🐝"]
            },
            theme5: {
                name: "Summer",
                background: "linear-gradient(to bottom, #ffba08, #ff9e00)",
                cardBg: "rgba(255, 255, 255, 0.85)",
                textColor: "#e85d04",
                highlightColor: "#dc2f02",
                heartColor: "#dc2f02",
                heartShadow: "0 5px 15px rgba(220, 47, 2, 0.5)",
                fallingItems: ["summer", 60, ["#ffba08", "#fcbf49", "#f48c06", "#fee440"]],
                doodles: ["☀️", "🌊", "🏖️", "🍉"]
            },
            theme6: {
                name: "Autumn",
                background: "linear-gradient(to bottom, #d56f3e, #9c6644)",
                cardBg: "rgba(255, 250, 240, 0.85)",
                textColor: "#774936",
                highlightColor: "#ae2012",
                heartColor: "#ae2012",
                heartShadow: "0 5px 15px rgba(174, 32, 18, 0.5)",
                fallingItems: ["leaf", 75, ["#e76f51", "#f4a261", "#e9c46a", "#ca6702"]],
                doodles: ["🍁", "🍂", "🦊", "🎃"]
            },
            theme7: {
                name: "Winter",
                background: "linear-gradient(to bottom, #457b9d, #1d3557)",
                cardBg: "rgba(255, 255, 255, 0.9)",
                textColor: "#1d3557",
                highlightColor: "#457b9d",
                heartColor: "#457b9d",
                heartShadow: "0 5px 15px rgba(69, 123, 157, 0.5)",
                fallingItems: ["snow", 85, ["#ffffff", "#f5f5f5", "#e5e5e5"]],
                doodles: ["❄️", "☃️", "⛄", "❄️"]
            },
            theme8: {
                name: "Forest",
                background: "linear-gradient(to bottom, #2d6a4f, #1b4332)",
                cardBg: "rgba(255, 250, 240, 0.85)",
                textColor: "#1b4332",
                highlightColor: "#40916c",
                heartColor: "#40916c",
                heartShadow: "0 5px 15px rgba(64, 145, 108, 0.5)",
                fallingItems: ["leaf", 70, ["#95d5b2", "#40916c", "#74c69d", "#b7e4c7"]],
                doodles: ["🌲", "🍄", "🦌", "🐿️"]
            }
        };
        
        // Collection of quotes - 100 quotes about love, wisdom, and advice
        const quotes = [
            "Love is composed of a single soul inhabiting two bodies.",
            "Where there is love, there is life.",
            "Being deeply loved by someone gives you strength, while loving someone deeply gives you courage.",
            "The best thing to hold onto in life is each other.",
            "Love is not about how many days, months, or years you have been together. It's about how much you love each other every day.",
            "I love you not because of who you are, but because of who I am when I am with you.",
            "Love is when the other person's happiness is more important than your own.",
            "The greatest happiness of life is the conviction that we are loved; loved for ourselves.",
            "To love and be loved is to feel the sun from both sides.",
            "Love isn't something you find. Love is something that finds you.",
            "The best love is the kind that awakens the soul and makes us reach for more.",
            "True love stories never have endings.",
            "Love is a friendship set to music.",
            "The greatest thing you'll ever learn is just to love and be loved in return.",
            "Love is the only force capable of transforming an enemy into a friend.",
            "If I know what love is, it is because of you.",
            "You know you're in love when you can't fall asleep because reality is finally better than your dreams.",
            "Love doesn't make the world go 'round. Love is what makes the ride worthwhile.",
            "A successful marriage requires falling in love many times, always with the same person.",
            "The giving of love is an education in itself.",
            "Love recognizes no barriers. It jumps hurdles, leaps fences, penetrates walls to arrive at its destination full of hope.",
            "The art of love is largely the art of persistence.",
            "Age does not protect you from love, but love to some extent protects you from age.",
            "Life is the flower for which love is the honey.",
            "We are most alive when we're in love.",
            "Love is the beauty of the soul.",
            "There is only one happiness in this life, to love and be loved.",
            "When we love, we always strive to become better than we are.",
            "Where there is love there is life.",
            "Love is an endless mystery, for it has nothing else to explain it.",
            "The greatest gift that you can give to others is the gift of unconditional love and acceptance.",
            "The best and most beautiful things in this world cannot be seen or even heard, but must be felt with the heart.",
            "There is no remedy for love but to love more.",
            "The heart wants what it wants. There's no logic to these things.",
            "Love is when you meet someone who tells you something new about yourself.",
            "Our lives begin to end the day we become silent about things that matter.",
            "The future belongs to those who believe in the beauty of their dreams.",
            "The only way to do great work is to love what you do.",
            "The journey of a thousand miles begins with one step.",
            "Believe you can and you're halfway there.",
            "What lies behind us and what lies before us are tiny matters compared to what lies within us.",
            "In three words I can sum up everything I've learned about life: it goes on.",
            "Life is 10% what happens to us and 90% how we react to it.",
            "Change your thoughts and you change your world.",
            "The purpose of our lives is to be happy.",
            "To live is the rarest thing in the world. Most people exist, that is all.",
            "Life isn't about finding yourself. Life is about creating yourself.",
            "Every moment is a fresh beginning.",
            "Life is what happens when you're busy making other plans.",
            "The two most important days in your life are the day you are born and the day you find out why.",
            "Life is really simple, but we insist on making it complicated.",
            "Don't count the days, make the days count.",
            "You only live once, but if you do it right, once is enough.",
            "Live as if you were to die tomorrow. Learn as if you were to live forever.",
            "It does not matter how slowly you go as long as you do not stop.",
            "Success is not final, failure is not fatal: It is the courage to continue that counts.",
            "The only impossible journey is the one you never begin.",
            "Life is either a daring adventure or nothing at all.",
            "Happiness is not something ready-made. It comes from your own actions.",
            "The greatest glory in living lies not in never falling, but in rising every time we fall.",
            "The way to get started is to quit talking and begin doing.",
            "Your time is limited, don't waste it living someone else's life.",
            "In the end, it's not the years in your life that count. It's the life in your years.",
            "Never let the fear of striking out keep you from playing the game.",
            "The mind is everything. What you think you become.",
            "Love the life you live. Live the life you love.",
            "Keep your face always toward the sunshine, and shadows will fall behind you.",
            "Many of life's failures are people who did not realize how close they were to success when they gave up.",
            "In order to write about life first you must live it.",
            "If life were predictable it would cease to be life, and be without flavor.",
            "The biggest adventure you can take is to live the life of your dreams.",
            "Life is a succession of lessons which must be lived to be understood.",
            "Life is never fair, and perhaps it is a good thing for most of us that it is not.",
            "The good life is one inspired by love and guided by knowledge.",
            "Life itself is the most wonderful fairy tale.",
            "Do not let making a living prevent you from making a life.",
            "Life is ours to be spent, not to be saved.",
            "Life is a long lesson in humility.",
            "The purpose of life is not to be happy. It is to be useful, to be honorable, to be compassionate.",
            "I have found that if you love life, life will love you back.",
            "We do not remember days, we remember moments.",
            "Life is short, and it is up to you to make it sweet.",
            "Keep smiling, because life is a beautiful thing and there's so much to smile about.",
            "A birthday is the beginning of a 365-day journey around the sun. Make it a great trip.",
            "Cherish all your happy moments: they make a fine cushion for old age.",
            "With mirth and laughter let old wrinkles come.",
            "Age is an issue of mind over matter. If you don't mind, it doesn't matter.",
            "The secret of staying young is to live honestly, eat slowly, and lie about your age.",
            "Youth has no age.",
            "Today you are you, that is truer than true. There is no one alive who is youer than you.",
            "You don't get older, you get better.",
            "We turn not older with years, but newer every day.",
            "Growing old is mandatory; growing up is optional.",
            "Each day is a gift that's why they call it the present.",
            "Sometimes the heart sees what is invisible to the eye.",
            "Shoot for the moon. Even if you miss, you'll land among the stars."
        ];
        
        // Get DOM elements
        const body = document.querySelector('body');
        const card = document.querySelector('.card');
        const title = document.querySelector('h1');
        const date = document.querySelector('.date');
        const heart = document.querySelector('.heart');
        const quoteDisplay = document.getElementById('quote-display');
        const doodles = [
            document.getElementById('doodle1'),
            document.getElementById('doodle2'),
            document.getElementById('doodle3'),
            document.getElementById('doodle4')
        ];
        
        // Keep track of falling items containers for cleanup
        let fallingItemsContainers = [];
        let currentQuoteIndex = 0;
        
        // Theme change function with ultra-smooth transitions
        function changeTheme(themeName) {
            const theme = themes[themeName];
            
            // Change background
            body.style.background = theme.background;
            
            // Change card styles
            card.style.backgroundColor = theme.cardBg;
            title.style.color = theme.textColor;
            date.style.color = theme.textColor;
            
            // Change heart colors
            heart.style.backgroundColor = theme.heartColor;
            heart.style.boxShadow = theme.heartShadow;
            
            // Update heart's pseudo-elements color
            document.documentElement.style.setProperty('--heart-color', theme.heartColor);
            
            // Update doodles
            for (let i = 0; i < doodles.length; i++) {
                doodles[i].textContent = theme.doodles[i];
                doodles[i].style.fontSize = '30px';
            }
            
            // Clean up previous falling items after transition delay
            setTimeout(() => {
                cleanupFallingItems();
                // Create new falling items
                createFallingItems(theme.fallingItems[0], theme.fallingItems[1], theme.fallingItems[2]);
            }, 4000);
        }
        
        // Create falling items
        function createFallingItems(type, count, colors) {
            const container = document.createElement('div');
            container.classList.add('falling-container');
            body.appendChild(container);
            fallingItemsContainers.push(container);
            
            for (let i = 0; i < count; i++) {
                const item = document.createElement('div');
                const size = Math.random() * 20 + 10;
                const color = colors[Math.floor(Math.random() * colors.length)];
                
                item.classList.add('falling');
                
                // Set common properties
                item.style.left = `${Math.random() * 100}vw`;
                item.style.animationDuration = `${Math.random() * 10 + 5}s`;
                item.style.animationDelay = `${Math.random() * 8}s`;
                
                // Set type-specific properties
                if (type === 'petal') {
                    item.style.width = `${size}px`;
                    item.style.height = `${size}px`;
                    item.style.backgroundColor = color;
                    item.style.borderRadius = '150% 0 150% 0';
                    item.style.transform = `rotate(${Math.random() * 360}deg)`;
                    item.style.filter = 'blur(1px)';
                } 
                else if (type === 'heart') {
                    item.innerHTML = '❤';
                    item.style.fontSize = `${size * 1.5}px`;
                    item.style.color = color;
                    item.style.opacity = '0.8';
                }
                else if (type === 'neon') {
                    item.style.width = `${size * 0.7}px`;
                    item.style.height = `${size * 0.7}px`;
                    item.style.backgroundColor = color;
                    item.style.borderRadius = '50%';
                    item.style.boxShadow = `0 0 ${size/2}px ${color}`;
                    item.style.filter = 'blur(1px)';
                }
                else if (type === 'flower') {
                    const flowers = ['🌸', '🌼', '🌺', '🌷', '🌻'];
                    item.innerHTML = flowers[Math.floor(Math.random() * flowers.length)];
                    item.style.fontSize = `${size}px`;
                    item.style.opacity = '0.9';
                }
                else if (type === 'summer') {
                    const summerItems = ['☀️', '🌴', '🌊', '✨', '🐚'];
                    item.innerHTML = summerItems[Math.floor(Math.random() * summerItems.length)];
                    item.style.fontSize = `${size}px`;
                    item.style.opacity = '0.9';
                }
                else if (type === 'leaf') {
                    const leaves = ['🍂', '🍁', '🍃'];
                    item.innerHTML = leaves[Math.floor(Math.random() * leaves.length)];
                    item.style.fontSize = `${size}px`;
                    item.style.opacity = '0.9';
                }
                else if (type === 'snow') {
                    item.style.width = `${size * 0.5}px`;
                    item.style.height = `${size * 0.5}px`;
                    item.style.backgroundColor = color;
                    item.style.borderRadius = '50%';
                    item.style.boxShadow = `0 0 ${size/3}px ${color}`;
                    item.style.opacity = '0.8';
                    item.style.filter = 'blur(0.5px)';
                }
                
                container.appendChild(item);
            }
        }
        
        // Clean up falling items
        function cleanupFallingItems() {
            fallingItemsContainers.forEach(container => {
                if (container && container.parentNode) {
                    container.parentNode.removeChild(container);
                }
            });
            fallingItemsContainers = [];
        }
        
        // Update quote display
        function updateQuote() {
            quoteDisplay.style.animation = 'none';
            void quoteDisplay.offsetWidth; // Trigger reflow
            quoteDisplay.textContent = quotes[currentQuoteIndex];
            quoteDisplay.style.animation = 'fadeInOut 10s linear';
            
            currentQuoteIndex = (currentQuoteIndex + 1) % quotes.length;
        }
        
        // Apply heart pseudo-element color changes
        const styleElement = document.createElement('style');
        styleElement.textContent = `
            .heart:before, .heart:after {
                background-color: var(--heart-color, #e74c3c);
            }
        `;
        document.head.appendChild(styleElement);
        
        // Auto rotation of themes with ultra-smooth transitions
        function startAutoRotation() {
            let themeKeys = Object.keys(themes);
            let currentIndex = 0;
            let currentTheme = themeKeys[currentIndex];
            
            // Set initial theme
            document.documentElement.style.setProperty('--heart-color', themes[currentTheme].heartColor);
            
            // Initial falling items
            createFallingItems(
                themes[currentTheme].fallingItems[0],
                themes[currentTheme].fallingItems[1],
                themes[currentTheme].fallingItems[2]
            );
            
            // Initial doodles
            for (let i = 0; i < doodles.length; i++) {
                doodles[i].textContent = themes[currentTheme].doodles[i];
                doodles[i].style.fontSize = '30px';
            }
            
            // Set up theme rotation
            setInterval(() => {
                currentIndex = (currentIndex + 1) % themeKeys.length;
                currentTheme = themeKeys[currentIndex];
                changeTheme(currentTheme);
            }, 12000); // Change theme every 12 seconds
            
            // Set up quote rotation
            updateQuote(); // Initial quote
            setInterval(updateQuote, 10000); // Change quote every 10 seconds
        }
        
        // Start the automatic theme rotation and quotes
        startAutoRotation();
    </script>
</body>
</html>
