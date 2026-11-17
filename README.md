index.html

<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="theme-color" content="#c9b5e8">
  <meta name="description" content="Un pequeño universo donde siempre hay un lugar para ti.">
  <link rel="manifest" href="./manifest.json">
  <title>Lunaria 🌙</title>

  <style>
    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      font-family: Georgia, serif;
      color: white;
      text-align: center;
      background: linear-gradient(145deg, #211632, #80649e, #d3c0e8);
    }

    main {
      padding: 30px;
    }

    h1 {
      font-size: 3.5rem;
      font-weight: normal;
      letter-spacing: 5px;
    }

    p {
      line-height: 1.8;
      font-style: italic;
    }

    .moon {
      font-size: 70px;
      animation: glow 3s infinite alternate;
    }

    button {
      margin-top: 25px;
      padding: 13px 25px;
      border: 1px solid white;
      border-radius: 30px;
      background: #ffffff25;
      color: white;
      font-size: 16px;
    }

    @keyframes glow {
      to {
        text-shadow: 0 0 30px white;
        transform: scale(1.08);
      }
    }
  </style>
</head>

<body>
  <main>
    <div class="moon">☾</div>
    <h1>Lunaria</h1>
    <p>Un pequeño universo donde siempre<br>hay un lugar para ti.</p>
    <p>Bienvenida a casa. ✨</p>
    <button id="install" hidden>Instalar Lunaria 🌙</button>
  </main>

  <script>
    if ("serviceWorker" in navigator) {
      window.addEventListener("load", () => {
        navigator.serviceWorker.register("./service-worker.js");
      });
    }

    let installPrompt;

    window.addEventListener("beforeinstallprompt", event => {
      event.preventDefault();
      installPrompt = event;
      document.getElementById("install").hidden = false;
    });

    document.getElementById("install").addEventListener("click", async () => {
      if (!installPrompt) return;
      installPrompt.prompt();
      await installPrompt.userChoice;
      installPrompt = null;
    });
  </script>
</body>
</html>
