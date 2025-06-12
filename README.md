<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Filtro de Color con Cámara</title>
  <style>
    body {
      margin: 0;
      background: #111;
      color: #fff;
      font-family: Arial, sans-serif;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
    }

    .camera-container {
      position: relative;
      max-width: 90vw;
      max-height: 80vh;
      overflow: hidden;
      border: 5px solid #444;
    }

    video {
      width: 100%;
      height: auto;
      display: block;
      transform: scaleX(-1); /* Para hacer el espejo horizontal de la cámara */
    }

    .filter {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      mix-blend-mode: multiply;
      pointer-events: none;
      transition: background-color 0.3s ease;
    }

    .buttons {
      margin-top: 20px;
    }

    .buttons button {
      margin: 0 10px;
      padding: 10px 20px;
      font-size: 16px;
      cursor: pointer;
      border: none;
      border-radius: 4px;
      background-color: #333;
      color: white;
    }

    .buttons button:hover {
      background-color: #555;
    }
  </style>
</head>
<body>

  <h1>Filtro de Color en Cámara</h1>

  <div class="camera-container">
    <video id="video" autoplay></video>
    <div class="filter" id="colorFilter"></div>
  </div>

  <div class="buttons">
    <button onclick="setFilter('red')">Rojo</button>
    <button onclick="setFilter('green')">Verde</button>
    <button onclick="setFilter('blue')">Azul</button>
    <button onclick="setFilter('none')">Sin Filtro</button>
  </div>

  <script>
    // Acceder a la cámara
    async function startCamera() {
      try {
        const stream = await navigator.mediaDevices.getUserMedia({
          video: true
        });
        const video = document.getElementById('video');
        video.srcObject = stream;
      } catch (err) {
        console.error("Error al acceder a la cámara: ", err);
      }
    }

    // Función para cambiar el filtro
    function setFilter(color) {
      const filter = document.getElementById("colorFilter");
      switch(color) {
        case 'red':
          filter.style.backgroundColor = 'rgba(255, 0, 0, 0.6)';
          break;
        case 'green':
          filter.style.backgroundColor = 'rgba(0, 255, 0, 0.6)';
          break;
        case 'blue':
          filter.style.backgroundColor = 'rgba(0, 0, 255, 0.6)';
          break;
        default:
          filter.style.backgroundColor = 'transparent';
      }
    }

    // Iniciar la cámara al cargar la página
    window.onload = startCamera;
  </script>

</body>
</html>
