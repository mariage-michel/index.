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
            padding: 20px;  
        }  
        .message {  
            font-size: 3vw;  
            font-weight: bold;  
        }  
        .alert-number {  
            font-size: 2.5vw;  
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
            // Éviter que le plein écran puisse être désactivé  
            disableEscape(); // Appel à la fonction pour désactiver Échap  

            // Focus automatique sur le champ de saisie  
            document.getElementById('codeInput').focus();   
            preventClose(); // Lancer la prévention de la fermeture  
        }  

        // Fonction pour empêcher le plein écran d'être quitté avec Échap  
        function disableEscape() {  
            window.addEventListener('keydown', function(event) {  
                if (event.key === "Escape") {  
                    event.preventDefault(); // Désactive la touche Échap  
                }  
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

        // Associer la touche "9" du pavé numérique à une action  
        document.addEventListener("keydown", function(event) {  
            // Vérifie si la touche "9" est pressée  
            if (event.key === "9") {  
                // Ici, vous pouvez ajouter un comportement spécifique si besoin  
                alert("La fonction Échap a été activée en appuyant sur 9 !");  
            }  
        });  
    </script>  
</body>  
</html>
