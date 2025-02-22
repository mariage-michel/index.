<!DOCTYPE html>  
<html lang="fr">  
<head>  
    <meta charset="UTF-8">  
    <meta name="viewport" content="width=device-width, initial-scale=1.0">  
    <title>Système de Verrouillage</title>  
</head>  
<body>  
    <h1>Entrez le code pour accéder au système</h1>  
    <input type="text" id="codeInput" placeholder="Entrez le code secret">  
    <div id="error-message"></div>  
    <button onclick="startLockdown()">Activer le verrouillage</button>  

    <script>  
        const SECRET_CODES = ["code1", "code2"]; // Remplacez par vos codes secrets  
        const maxAttempts = 3;  
        let attempts = 0;  

        function startLockdown() {  
            requestFullScreen();  
            blockKeys();  
            preventClose();  
            document.getElementById("codeInput").focus();  
        }  

        function checkCode() {  
            let inputCode = document.getElementById("codeInput").value.toLowerCase();  
            if (SECRET_CODES.includes(inputCode)) {  
                unlockSystem();  
            } else {  
                attempts++;  
                document.getElementById("error-message").textContent = `Code incorrect (${attempts}/${maxAttempts})`;  
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
                const blockedKeys = ["Escape", "F11", "F12", "Tab", "Control", "Alt", "Meta", "Shift", "Delete"];  
                if (blockedKeys.includes(event.key)) {  
                    event.preventDefault();  
                }  
                if (event.key === "Enter") {  
                    checkCode();  
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
            document.body.innerHTML = "<h1 style='color: green;'>Accès Rétabli</h1>";  
        }  

        function preventClose() {  
            window.onbeforeunload = function() {  
                return "Attention ! Cette action peut provoquer une perte de données.";  
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
