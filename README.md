<html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy Birthday Hana!</title>
    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@700&family=Montserrat:wght@400;700&display=swap" rel="stylesheet">
    <style>
        body {
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            font-family: 'Montserrat', sans-serif;
            overflow: hidden;
            background-color: #f5f5f5;
            transition: background-color 1.5s ease;
        }

        .night-sky {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            opacity: 0;
            transition: opacity 2s ease;
        }

        .star {
            position: absolute;
            background-color: #fff;
            border-radius: 50%;
            animation: twinkle 1.5s infinite alternate;
        }

        @keyframes twinkle {
            0% { opacity: 0.3; }
            100% { opacity: 1; }
        }

        /* Envelope Styles */
        .envelope {
            width: 300px;
            height: 200px;
            background-color: #f8d486;
            position: relative;
            cursor: pointer;
            box-shadow: 0 15px 35px rgba(255, 244, 181, 0.9);
            transition: all 0.8s cubic-bezier(0.68, -0.55, 0.27, 1.55);
            z-index: 10;
            transform-style: preserve-3d;
        }

        .envelope:before {
            content: '';
            position: absolute;
            top: 0;
            width: 0;
            height: 0;
            border-left: 150px solid transparent;
            border-right: 150px solid transparent;
            border-top: 100px solid #f5c34a;
            transform-origin: top;
            transform: rotateX(0deg);
            transition: all 0.8s cubic-bezier(0.68, -0.55, 0.27, 1.55) 0.3s;
            z-index: 5;
        }

        .envelope.open:before {
            transform: rotateX(180deg);
        }

        .envelope.open {
            transform: translateY(100px) rotateX(10deg);
            box-shadow: 0 15px 35px rgba(255, 244, 181, 0.9);
        }

        .envelope.fade-out {
            opacity: 0;
            transform: translateY(100px) scale(0.9);
            transition: all 0.8s ease;
        }

        /* Letter Styles */
        .letter {
            position: absolute;
            width: 280px;
            height: 180px;
            background-color: white;
            top: 10px;
            left: 10px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            font-size: 22px;
            font-weight: bold;
            color: #333;
            transition: all 0.8s cubic-bezier(0.68, -0.55, 0.27, 1.55) 0.5s;
            opacity: 0;
            transform: translateY(-20px);
            box-shadow: 0 2px 10px rgba(0,0,0,0.2);
        }

        .envelope.open .letter {
            opacity: 1;
            transform: translateY(0);
        }

        /* Clover Emoji Styles */
        .clover {
            font-size: 32px;
            opacity: 0;
            transition: opacity 1s ease 1s;
            animation: gentlePulse 3s ease-in-out infinite;
        }

        .envelope.open .letter .clover {
            opacity: 1;
        }

        @keyframes gentlePulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.2); }
        }

        /* Slot Machine Styles */
        .slot-machine {
            position: absolute;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            background-color: rgba(0, 0, 0, 0.8);
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 0 30px rgba(255, 215, 0, 0.7);
            z-index: 9;
            opacity: 0;
            transform: translateY(30px) scale(0.95);
            transition: all 0.8s cubic-bezier(0.68, -0.55, 0.27, 1.55) 0.3s;
            pointer-events: none;
        }

        .slot-machine.show {
            opacity: 1;
            transform: translateY(0) scale(1);
            z-index: 90;
            pointer-events: all;
        }

        .slot-title {
            color: gold;
            font-size: 24px;
            margin-bottom: 20px;
            text-align: center;
        }

        .slot-display {
            display: flex;
            justify-content: center;
            gap: 10px;
            margin-bottom: 20px;
        }

        .slot-column {
            display: flex;
            flex-direction: column;
            align-items: center;
            width: 60px;
            height: 100px;
            overflow: hidden;
            background-color: #222;
            border-radius: 5px;
            position: relative;
        }

        .slot-number {
            width: 100%;
            height: 100px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 40px;
            color: white;
            font-weight: bold;
            transition: transform 0.3s ease;
        }

        .slot-separator {
            font-size: 40px;
            color: gold;
            display: flex;
            align-items: center;
        }

        /* Birthday Cake Styles */
        .birthday-cake {
            position: absolute;
            display: none;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            z-index: 100;
            text-align: center;
            opacity: 0;
            transition: opacity 1s ease 0.5s;
        }

        .birthday-cake.show {
            opacity: 1;
        }

        .cake-container {
            position: relative;
            width: 220px;
            height: 250px;
            margin-bottom: 30px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .birthday-message {
            font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
            font-size: 32px;
            color: #fff;
            text-shadow: 0 0 10px #ffbbdd, 0 0 20px #ff69b4;
            font-weight: bold;
            animation: glow 2s infinite alternate, float 3s ease-in-out infinite;
            margin-bottom: 20px;
            z-index: 101;
            position: relative;
            opacity: 0;
            transform: translateY(20px);
            transition: all 0.8s ease 0.3s;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }

        @keyframes glow {
            from { text-shadow: 0 0 10px #ffbbdd, 0 0 20px #ff69b4; }
            to { text-shadow: 0 0 20px #da5597, 0 0 30px #ff78bb, 0 0 40px #ff69b4; }
        }

        .birthday-cake.show .birthday-message {
            opacity: 1;
            transform: translateY(0);
        }

        .cake {
            position: absolute;
            width: 200px;
            height: 100px;
            background: #f7c5d1;
            border-radius: 50% / 20%;
            border-bottom: 20px solid #b87f50;
            left: 50%;
            transform: translateX(-50%);
            bottom: 0;
            opacity: 0;
            transition: all 0.8s ease;
        }

        .icing {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 60%;
            background: #ff99bb;
            border-radius: 50% / 20%;
        }

        .drips {
            position: absolute;
            top: 40px;
            left: 10px;
            width: 180px;
            height: 30px;
            background: transparent;
        }

        .drip {
            position: absolute;
            width: 20px;
            height: 30px;
            background: #ff99bb;
            border-radius: 10px;
        }

        .drip:nth-child(1) { left: 10px; height: 20px; }
        .drip:nth-child(2) { left: 40px; height: 30px; }
        .drip:nth-child(3) { left: 80px; height: 25px; }
        .drip:nth-child(4) { left: 120px; height: 30px; }
        .drip:nth-child(5) { left: 150px; height: 20px; }

        .candle {
            position: absolute;
            top: -20px;
            left: 50%;
            width: 10px;
            height: 40px;
            background: red;
            border-radius: 5px;
            transform: translateX(-50%);
            opacity: 0;
            transition: all 0.5s ease 0.5s;
        }

        .flame {
            position: absolute;
            top: -15px;
            left: 50%;
            width: 12px;
            height: 18px;
            background: orange;
            border-radius: 50%;
            transform: translateX(-50%);
            animation: flicker 0.5s infinite alternate;
        }

        @keyframes flicker {
            0%, 100% { transform: translateX(-50%) scale(1); opacity: 1; }
            50% { transform: translateX(-50%) scale(1.1); opacity: 0.8; }
        }

        .birthday-cake.show .cake,
        .birthday-cake.show .candle {
            opacity: 1;
        }

        /* Golden Star Notification */
        .golden-star {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 60px;
            color: gold;
            text-shadow: 0 0 20px rgba(255, 215, 0, 0.8);
            cursor: pointer;
            opacity: 0;
            z-index: 150;
            animation: pulse 2s infinite, float 3s ease-in-out infinite;
            transition: all 0.5s ease;
        }

        .golden-star.visible {
            opacity: 1;
        }

        .birthday-message-container {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 80%;
            max-width: 500px;
            background: rgba(0, 0, 0, 0.85);
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 0 30px rgba(255, 215, 0, 0.5);
            color: white;
            font-family: 'Dancing Script', cursive;
            font-size: 22px;
            line-height: 1.6;
            text-align: center;
            opacity: 0;
            z-index: 200;
            pointer-events: none;
            transition: all 0.8s ease;
        }

        .birthday-message-container.visible {
            opacity: 1;
            pointer-events: all;
        }

        .birthday-message-container p {
            margin: 15px 0;
        }

        .final-confetti {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 180;
            pointer-events: none;
        }

        .fade-out {
            opacity: 0;
            transition: opacity 1s ease;
        }

        @keyframes pulse {
            0% { transform: translate(-50%, -50%) scale(1); }
            50% { transform: translate(-50%, -50%) scale(1.2); }
            100% { transform: translate(-50%, -50%) scale(1); }
        }

        .confetti {
            position: absolute;
            width: 10px;
            height: 10px;
            background-color: #f00;
            opacity: 0;
        }
    </style>
</head>
<body>
    <div class="night-sky" id="night-sky"></div>
    
    <div class="envelope" id="envelope">
        <div class="letter">
            <div class="letter-text">Welcome to Life 2025</div>
            <div class="clover">🍀</div>
        </div>
    </div>

    <!-- Slot Machine Scene -->
    <div class="slot-machine" id="slot-machine">
        <div class="slot-title">Your Special Date</div>
        <div class="slot-display">
            <div class="slot-column" id="day-column">
                <div class="slot-number">0</div>
                <div class="slot-number">0</div>
            </div>
            <div class="slot-separator">/</div>
            <div class="slot-column" id="month-column">
                <div class="slot-number">0</div>
                <div class="slot-number">0</div>
            </div>
            <div class="slot-separator">/</div>
            <div class="slot-column" id="year-column">
                <div class="slot-number">0</div>
                <div class="slot-number">0</div>
            </div>
        </div>
    </div>

    <!-- Birthday Cake Scene -->
    <div class="birthday-cake" id="birthday-cake">
        <div class="cake-container">
            <div class="birthday-message">Happy Level Up!</div>
            <div class="cake">
                <div class="icing"></div>
                <div class="drips">
                    <div class="drip"></div>
                    <div class="drip"></div>
                    <div class="drip"></div>
                    <div class="drip"></div>
                    <div class="drip"></div>
                </div>
                <div class="candle">
                    <div class="flame"></div>
                </div>
            </div>
        </div>
    </div>

    <!-- Golden Star Notification -->
    <div class="golden-star" id="golden-star">⭐</div>
    
    <!-- Birthday Message -->
    <div class="birthday-message-container" id="birthday-message">
        <p>I hope you see how incredible and cool you are.</p>
        <p>I hope you keep shooting for the stars every day.</p>
        <p>I hope you know that you are super, daring and amazing.</p>
        <p>And I hope that you are happy.</p>
        <p>happy birthday.</p>
    </div>
    
    <!-- Final Confetti Container -->
    <div class="final-confetti" id="final-confetti"></div>

    <script>
        // Create stars
        function createStars() {
            const nightSky = document.getElementById('night-sky');
            for (let i = 0; i < 200; i++) {
                const star = document.createElement('div');
                star.className = 'star';
                
                const size = Math.random() * 3;
                star.style.width = `${size}px`;
                star.style.height = `${size}px`;
                
                star.style.left = `${Math.random() * 100}%`;
                star.style.top = `${Math.random() * 100}%`;
                
                star.style.animationDelay = `${Math.random() * 2}s`;
                star.style.animationDuration = `${0.5 + Math.random() * 2}s`;
                
                nightSky.appendChild(star);
            }
        }
        
        createStars();

        const envelope = document.getElementById('envelope');
        const slotMachine = document.getElementById('slot-machine');
        
        envelope.addEventListener('click', () => {
            // Open envelope
            envelope.classList.add('open');
            
            setTimeout(() => {
                envelope.classList.add('fade-out');
                slotMachine.classList.add('show');
                
                setTimeout(() => {
                    animateSlotMachine();
                }, 300);
                
            }, 3500);
        });

        // Slot machine animation
        function animateSlotMachine() {
            const dayColumn = document.getElementById('day-column');
            const monthColumn = document.getElementById('month-column');
            const yearColumn = document.getElementById('year-column');
            
            const targetDay = [2, 7];
            const targetMonth = [0, 7];
            const targetYear = [2, 5];

            function animateColumn(column, targetNumbers, index, callback) {
                const numbers = column.querySelectorAll('.slot-number');
                let spins = 0;
                const maxSpins = 10 + index * 5;
                const spinInterval = 100 + index * 50;
                
                const spin = setInterval(() => {
                    numbers[0].textContent = Math.floor(Math.random() * 3);
                    numbers[1].textContent = Math.floor(Math.random() * 9);

                    spins++;
                    
                    if (spins >= maxSpins) {
                        clearInterval(spin);
                        numbers[0].textContent = targetNumbers[0];
                        numbers[1].textContent = targetNumbers[1];
                        
                        numbers[0].style.transform = 'scale(1.2)';
                        numbers[1].style.transform = 'scale(1.2)';
                        setTimeout(() => {
                            numbers[0].style.transform = 'scale(1)';
                            numbers[1].style.transform = 'scale(1)';
                        }, 300);
                        
                        if (callback) callback();
                    }
                }, spinInterval);
            }
            
            animateColumn(dayColumn, targetDay, 0, () => {
                animateColumn(monthColumn, targetMonth, 1, () => {
                    animateColumn(yearColumn, targetYear, 2, () => {
                        setTimeout(() => {
                            document.body.style.backgroundColor = '#0a0a2a';
                            document.getElementById('night-sky').style.opacity = '1';
                            
                            createConfetti();
                            
                            slotMachine.classList.remove('show');
                            
                            setTimeout(() => {
                                const cake = document.getElementById('birthday-cake');
                                cake.style.display = 'flex';
                                setTimeout(() => {
                                    cake.classList.add('show');
                                    
                                    // After 5 seconds, show golden star
                                    setTimeout(() => {
                                        cake.classList.add('fade-out');
                                        
                                        setTimeout(() => {
                                            document.getElementById('golden-star').classList.add('visible');
                                        }, 1000);
                                    }, 5000);
                                }, 50);
                            }, 800);
                        }, 2000);
                    });
                });
            });
        }

        // Golden star click handler
        document.getElementById('golden-star').addEventListener('click', function() {
            const goldenStar = this;
            const birthdayMessage = document.getElementById('birthday-message');
            
            goldenStar.classList.remove('visible');
            birthdayMessage.classList.add('visible');
            
            createConfetti(true);
        });

        // Confetti function
        function createConfetti(continuous = false) {
            const colors = ['#ff0000', '#ffff00', '#00ff00', '#00ffff', '#0000ff'];
            const confettiContainer = document.getElementById('final-confetti');
            
            // Clear previous confetti
            confettiContainer.innerHTML = '';
            
            // Big burst of confetti
            for (let i = 0; i < 150; i++) {
                setTimeout(() => {
                    const confetti = document.createElement('div');
                    confetti.className = 'confetti';
                    confetti.style.left = Math.random() * 100 + 'vw';
                    confetti.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
                    confetti.style.opacity = '1';
                    
                    // Random shape
                    if (Math.random() > 0.5) {
                        confetti.style.borderRadius = '50%';
                    }
                    
                    // Random size
                    const size = Math.random() * 10 + 5;
                    confetti.style.width = size + 'px';
                    confetti.style.height = size + 'px';
                    
                    confettiContainer.appendChild(confetti);
                    
                    // Animation
                    const animation = confetti.animate([
                        { transform: 'translateY(-100vh) rotate(0deg)', opacity: 1 },
                        { transform: `translateY(${window.innerHeight}px) rotate(${Math.random() * 360}deg)`, opacity: 0 }
                    ], {
                        duration: Math.random() * 3000 + 2000,
                        easing: 'cubic-bezier(0.1, 0.8, 0.9, 1)'
                    });
                    
                    // Remove after animation
                    animation.onfinish = () => {
                        confetti.remove();
                    };
                }, Math.random() * 500);
            }
            
            if (continuous) {
                // Continuous smaller confetti
                const interval = setInterval(() => {
                    for (let i = 0; i < 10; i++) {
                        const confetti = document.createElement('div');
                        confetti.className = 'confetti';
                        confetti.style.left = Math.random() * 100 + 'vw';
                        confetti.style.backgroundColor = '#ffff00';
                        confetti.style.opacity = '1';
                        confetti.style.borderRadius = '50%';
                        
                        const size = Math.random() * 8 + 4;
                        confetti.style.width = size + 'px';
                        confetti.style.height = size + 'px';
                        
                        confettiContainer.appendChild(confetti);
                        
                        const animation = confetti.animate([
                            { transform: 'translateY(-100vh) rotate(0deg)', opacity: 1 },
                            { transform: `translateY(${window.innerHeight}px) rotate(${Math.random() * 360}deg)`, opacity: 0 }
                        ], {
                            duration: Math.random() * 3000 + 2000,
                            easing: 'cubic-bezier(0.1, 0.8, 0.9, 1)'
                        });
                        
                        animation.onfinish = () => {
                            confetti.remove();
                        };
                    }
                }, 300);
                
                // Store interval ID to clear if needed
                confettiContainer.dataset.interval = interval;
            }
        }
    </script>
</body>
</html>
