# Giving Up the Game
Web, 100 points

## Description:
I can't wait to reveal this one! I have spent the entire summer working up an awesome game called Space Adventure! It's a bullet storm arcade shooter with survival horror elements and looter shooter portions heavily inspired by classics like Qubort, Donkey King, and Street Flighter II. Except this game isn't like other games - the only way to win is to cheat! Good luck!

## Solution:
We visit the website and get the following page:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Game Loading...</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #1b1b1b;
            color: #fff;
            text-align: center;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        .loading-container {
            text-align: center;
        }

        #loading-text {
            font-size: 2rem;
            color: #00ff00;
            animation: blink 1.5s infinite;
        }

        .loading-bar-container {
            width: 80%;
            max-width: 600px;
            background-color: #444;
            border: 2px solid #00ff00;
            border-radius: 10px;
            height: 30px;
            margin-top: 20px;
            position: relative;
            overflow: hidden;
        }

        .loading-bar {
            height: 100%;
            background-color: #00ff00;
            width: 0;
            animation: progressBar 300s linear forwards;
        }

        @keyframes blink {
            0% { opacity: 1; }
            50% { opacity: 0.5; }
            100% { opacity: 1; }
        }

        @keyframes progressBar {
            0% { width: 0%; }
            100% { width: 100%; }
        }

        .loading-spinner {
            margin-top: 30px;
            border: 8px solid #444;
            border-top: 8px solid #00ff00;
            border-radius: 50%;
            width: 80px;
            height: 80px;
            animation: spin 12s linear infinite;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .fake-tips {
            margin-top: 40px;
            font-size: 1.2rem;
            color: #fff;
        }
    </style>
</head>
<body>

<div class="loading-container">
    <div id="loading-text">Loading Space Adventure... Please wait.</div>

    <div class="loading-bar-container">
        <div class="loading-bar"></div>
    </div>

    <div class="loading-spinner"></div>

    <div class="fake-tips">Tip: Collect all power-ups to upgrade your ship! 💥</div>
</div>

<script>
    const tips = [
        "Tip: Collect all power-ups to upgrade your ship! 💥",
        "Tip: Watch out for asteroids in Sector 7! 🪨",
        "Tip: Shields down! Restore power to your defenses! ⚡",
        "Tip: New ship parts available at the space station! 🚀",
        "Tip: Find the hidden treasure on Planet Zog! 🌌"
    ];

    let tipIndex = 0;
    const tipElement = document.querySelector('.fake-tips');

    setInterval(() => {
        tipIndex = (tipIndex + 1) % tips.length;
        tipElement.textContent = tips[tipIndex];
    }, 7000); // Change tips every 7 seconds
        fetch('/getSprites')
            .then(response => response.json())
            .then(data => {
                console.log("VGhhbmsgeW91IE1hcmlvISBCdXQgb3VyIHByaW5jZXNzIGlzIGluIGFub3RoZXIgY2FzdGxlIQ==");
            });       
    </script>
</body>
</html>
```

When opening the console we see a base64 encoded string:
``VGhhbmsgeW91IE1hcmlvISBCdXQgb3VyIHByaW5jZXNzIGlzIGluIGFub3RoZXIgY2FzdGxlIQ==`` which decodes to: ``Thank you Mario! But our princess is in another castle!``

Looking closer at the code, we notice that the program also fetches ``/getSprites``

Navigating to that page, we see another base64-encoded string:
``"cG9jdGZ7dXdzcF8xXzdIMW5rXzdIM3IzcjBfMV80bX0="``

Decoding this string reveals the flag:

The flag: ``poctf{uwsp_1_7H1nk_7H3r3r0_1_4m}``
