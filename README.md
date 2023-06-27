<!DOCTYPE html>
<html>
<head>
  <title>Página con Funcionalidades de IA</title>
  <style>
    /* Estilos CSS para el escaneo y animaciones */
    .container {
      position: relative;
      width: 300px;
      height: 300px;
      border: 1px solid black;
      overflow: hidden;
    }

    .scan-line {
      position: absolute;
      top: 0;
      left: -100%;
      width: 100%;
      height: 2px;
      background-color: red;
      animation: scan-animation 4s linear infinite;
    }

    @keyframes scan-animation {
      0% { left: -100%; }
      100% { left: 100%; }
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="scan-line"></div>
  </div>

  <div>
    <textarea id="inputText" placeholder="Escribe aquí..."></textarea>
    <button id="speakButton">Hablar</button>
    <button id="stopButton">Detener</button>
    <p id="outputText"></p>
  </div>

  <script>
    // Función para mover la línea de escaneo
    function moveScanLine() {
      const scanLine = document.querySelector('.scan-line');
      scanLine.style.top = '0';
      scanLine.style.left = '-100%';
      scanLine.style.animation = 'scan-animation 4s linear infinite';
    }

    // Accedemos a la API de reconocimiento de voz del navegador
    const recognition = new (window.SpeechRecognition || window.webkitSpeechRecognition || window.mozSpeechRecognition || window.msSpeechRecognition)();

    // Configuramos el reconocimiento de voz
    recognition.lang = 'es-ES'; // Idioma del reconocimiento (español en este caso)

    // Evento que se ejecuta cuando se detecta el resultado del reconocimiento de voz
    recognition.onresult = function(event) {
      const speechResult = event.results[0][0].transcript;
      document.getElementById('outputText').textContent = speechResult;
    };

    // Eventos para iniciar y detener el reconocimiento de voz
    document.getElementById('speakButton').addEventListener('click', function() {
      recognition.start();
      moveScanLine();
    });

    document.getElementById('stopButton').addEventListener('click', function() {
      recognition.stop();
    });
  </script>
</body>
</html>

