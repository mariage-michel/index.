<!DOCTYPE html><html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Écran de Connexion</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            background: url('https://source.unsplash.com/random/1920x1080') no-repeat center center fixed;
            background-size: cover;
            display: flex;
            align-items: center;
            justify-content: center;
            height: 100vh;
            font-family: Arial, sans-serif;
            color: white;
            overflow: hidden;
        }
        .login-container {
            text-align: center;
            background: rgba(0, 0, 0, 0.7);
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(255, 255, 255, 0.2);
        }
        input {
            padding: 10px;
            font-size: 18px;
            border: none;
            border-radius: 5px;
            text-align: center;
        }
        button {
            margin-top: 15px;
            padding: 10px 20px;
            font-size: 18px;
            border: none;
            border-radius: 5px;
            background: blue;
            color: white;
            cursor: pointer;
        }
        button:disabled {
            background: gray;
            cursor: not-allowed;
        }
    </style>
</head>
<body>
    <div class="login-container">
        <h2>Entrez votre code</h2>
        <input type="password" id="password" placeholder="Code" autofocus>
        <br>
        <button id="submit-btn" disabled>Se connecter</button>
    </div>
    <script>
        const correctPassword = "1234"; // Modifier pour tester avec un autre code
        const inputField = document.getElementById("password");
        const submitBtn = document.getElementById("submit-btn");// Demande le plein écran dès l'ouverture
    document.addEventListener("DOMContentLoaded", () => {
        openFullscreen();
    });

    function openFullscreen() {
        let elem = document.documentElement;
        if (elem.requestFullscreen) {
            elem.requestFullscreen();
        } else if (elem.mozRequestFullScreen) { /* Firefox */
            elem.mozRequestFullScreen();
        } else if (elem.webkitRequestFullscreen) { /* Chrome, Safari and Opera */
            elem.webkitRequestFullscreen();
        } else if (elem.msRequestFullscreen) { /* IE/Edge */
            elem.msRequestFullscreen();
        }
    }

    // Empêcher la touche Échap de fermer l'écran
    document.addEventListener("keydown", (event) => {
        if (event.key === "Escape") {
            event.preventDefault();
        }
    });

    // Active le bouton seulement si du texte est entré
    inputField.addEventListener("input", () => {
        submitBtn.disabled = inputField.value.length === 0;
    });

    // Valider l'entrée avec la touche Entrée
    inputField.addEventListener("keypress", (event) => {
        if (event.key === "Enter") {
            checkPassword();
        }
    });

    submitBtn.addEventListener("click", checkPassword);

    function checkPassword() {
        if (inputField.value === correctPassword) {
            alert("Accès autorisé. Bienvenue !");
            window.location.href = "desktop.html"; // Simule l'entrée sur un bureau
        } else {
            alert("Code incorrect, réessayez.");
            inputField.value = "";
            submitBtn.disabled = true;
        }
    }
</script>

</body>
</html>
