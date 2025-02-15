<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Surprise</title>
    <style>
        body {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            height: 100vh;
            text-align: center;
            font-family: 'Poppins', sans-serif;
            background: linear-gradient(180deg, #ffdde1, #ee9ca7);
            overflow: hidden;
            position: relative;
        }
        .box {
            width: 150px;
            height: 150px;
            background: linear-gradient(135deg, #ff4d6d, #ff9aa2);
            display: flex;
            justify-content: center;
            align-items: center;
            color: white;
            font-size: 20px;
            font-weight: bold;
            cursor: pointer;
            border-radius: 20px;
            position: relative;
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.4);
            transition: transform 0.3s, box-shadow 0.3s, background 0.3s;
        }
        .box:hover {
            transform: scale(1.1);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.5);
        }
        .ribbon {
            width: 100px;
            height: 30px;
            background: red;
            position: absolute;
            top: -15px;
            left: 50%;
            transform: translateX(-50%) rotate(-20deg);
            text-align: center;
            color: white;
            font-size: 14px;
            font-weight: bold;
            line-height: 30px;
            border-radius: 5px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.3);
        }
        .shake {
            animation: shake 0.2s ease-in-out 3;
        }
        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-5px); }
            50% { transform: translateX(5px); }
            75% { transform: translateX(-5px); }
        }
        .open-box {
            animation: openBox 0.7s ease-in-out forwards;
        }
        @keyframes openBox {
            0% { transform: scale(1); opacity: 1; }
            50% { transform: scale(1.3) rotate(10deg); }
            100% { transform: scale(0); opacity: 0; }
        }
        .message {
            display: none;
            font-size: 28px;
            font-weight: bold;
            color: #ff2e63;
            margin-top: 20px;
            opacity: 0;
            transform: scale(0.8);
            transition: opacity 2s ease-in-out, transform 1.5s ease-in-out;
            position: relative;
        }
        .message.show {
            opacity: 1;
            transform: scale(1);
            animation: fadeInScale 1.5s ease-in-out forwards;
        }
        @keyframes fadeInScale {
            0% { opacity: 0; transform: scale(0.8); }
            100% { opacity: 1; transform: scale(1); }
        }
        .flower {
            position: fixed;
            font-size: 24px;
            opacity: 0.8;
            animation: fall 4s linear infinite;
            z-index: 100;
        }
        @keyframes fall {
            0% { transform: translateY(-100px) rotate(0deg); opacity: 1; }
            100% { transform: translateY(100vh) rotate(360deg); opacity: 0; }
        }
    </style>
</head>
<body>
    <div class="box" id="box">
        <div class="ribbon">For You 🎀</div>
        Click Me!
    </div>
    <div class="message" id="message"></div>
    
    <script>
        let clickCount = 0;
        const box = document.getElementById("box");
        const message = document.getElementById("message");
        const words = ["Sige pa!", "Click mo pa!", "One More!", "Excited?", "Last Click!"];
        const finalMessages = [
            "Hello, SSG President!🌸",
            "I just wanted to say I wish I was there to watch your movie...🎥",
            "I know you worked hard on it, and I'm sure it's amazing!🌟",
            "But I wanted to study a bit of coding and earn some money...",
            "Just so I can do this for you hahaha",
            "Sorry if it's not much, hindi ako magaling sa programming 🥺",
            "But ginawa ko to para lang sayo so...🤷‍♂️",
            "Happy Valentine's Day, Ness!💛"
        ];

        box.addEventListener("click", function() {
            clickCount++;
            box.classList.add("shake");
            setTimeout(() => {
                box.classList.remove("shake");
            }, 600);

            if (clickCount < 5) {
                box.textContent = words[clickCount - 1];
            }

            if (clickCount >= 5) {
                box.classList.add("open-box");
                setTimeout(() => {
                    box.style.display = "none";
                    message.style.display = "block";
                    let messageIndex = 0;
                    function showNextMessage() {
                        if (messageIndex < finalMessages.length) {
                            message.style.opacity = 0;
                            setTimeout(() => {
                                message.textContent = finalMessages[messageIndex];
                                message.classList.remove("show");
                                void message.offsetWidth;
                                message.classList.add("show");
                                messageIndex++;
                                setTimeout(showNextMessage, 2500);
                            }, 800);
                        } else {
                            createFlowerShower();
                        }
                    }
                    showNextMessage();
                }, 700);
            }
        });

        function createFlowerShower() {
            setInterval(() => {
                for (let i = 0; i < 5; i++) {
                    let flower = document.createElement("div");
                    flower.classList.add("flower");
                    flower.textContent = "🌸";
                    flower.style.left = Math.random() * 100 + "vw";
                    flower.style.animationDuration = (Math.random() * 2 + 2) + "s";
                    flower.style.top = "0";
                    document.body.appendChild(flower);
                    setTimeout(() => flower.remove(), 4000);
                }
            }, 500);
        }
    </script>
</body>
</html>
