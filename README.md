<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Sai Predictions</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Great+Vibes&family=Pacifico&display=swap');

    body {
      margin: 0;
      height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      font-family: 'Segoe UI', sans-serif;
      color: white;
      overflow: hidden;
    }
    video.bg-video {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      object-fit: cover;
      z-index: -2;
    }
    .overlay {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 30, 0.5);
      z-index: -1;
    }
    h1 {
      margin-bottom: 20px;
      font-size: 3.5rem;
      font-family: 'Great Vibes', cursive;
      color: #ffe6ff;
      text-shadow: 0 0 15px #ff33cc, 0 0 30px #cc00ff, 0 0 45px #6600ff;
      animation: glow 3s ease-in-out infinite alternate;
    }
    @keyframes glow {
      from { text-shadow: 0 0 10px #ff99ff, 0 0 20px #ff33cc, 0 0 30px #cc00ff; }
      to { text-shadow: 0 0 20px #ff66ff, 0 0 40px #cc33ff, 0 0 60px #9900ff; }
    }
    canvas {
      border-radius: 50%;
      box-shadow: 0 0 20px rgba(255,255,255,0.7);
      background: rgba(0, 0, 0, 0.6);
    }
    .pointer {
      position: absolute;
      top: 100px;
      left: 50%;
      transform: translateX(-50%);
      width: 0;
      height: 0;
      border-left: 20px solid transparent;
      border-right: 20px solid transparent;
      border-bottom: 40px solid gold;
      filter: drop-shadow(0 0 5px black);
    }
    button {
      margin-top: 30px;
      padding: 12px 25px;
      font-size: 1.1rem;
      border: none;
      border-radius: 10px;
      background: gold;
      color: black;
      font-weight: bold;
      cursor: pointer;
      transition: 0.3s;
    }
    button:hover {
      background: #ffd700;
      transform: scale(1.05);
    }
    .result {
      margin-top: 20px;
      font-size: 1.5rem;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <video autoplay muted loop class="bg-video">
    <source src="[# Spin-wheel-](https://www.vecteezy.com/members/ezstudio/uploads" type="video/mp4">
  </video>
  <div class="overlay"></div>

  <h1>🌌 Sai Predictions 🌌</h1>
  <div class="pointer"></div>
  <canvas id="wheel" width="500" height="500"></canvas>
  <button onclick="spinWheel()">Spin</button>
  <div class="result" id="result"></div>

  <script>
    const canvas = document.getElementById("wheel");
    const ctx = canvas.getContext("2d");
    const slices = 100;
    const sliceAngle = (2 * Math.PI) / slices;
    let currentRotation = 0;
    let spinning = false;

    function drawWheel() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      for (let i = 0; i < slices; i++) {
        const angle = i * sliceAngle + currentRotation;

        // Color slices
        ctx.beginPath();
        ctx.moveTo(250, 250);
        ctx.arc(250, 250, 250, angle, angle + sliceAngle);
        ctx.closePath();
        ctx.fillStyle = `hsl(${(i * 360) / slices}, 100%, 50%)`;
        ctx.fill();

        // Add numbers (bigger size)
        ctx.save();
        ctx.translate(250, 250);
        ctx.rotate(angle + sliceAngle / 2);
        ctx.textAlign = "right";
        ctx.fillStyle = "white";
        ctx.font = "bold 16px Segoe UI";
        ctx.fillText(i + 1, 230, 5);
        ctx.restore();
      }
    }

    function spinWheel() {
      if (spinning) return;
      spinning = true;
      const spinAngle = Math.random() * 2000 + 3000;
      const duration = 5000;
      const start = performance.now();

      function animate(time) {
        const elapsed = time - start;
        if (elapsed < duration) {
          const progress = elapsed / duration;
          const easeOut = 1 - Math.pow(1 - progress, 3);
          currentRotation = spinAngle * easeOut;
          drawWheel();
          requestAnimationFrame(animate);
        } else {
          spinning = false;
          currentRotation %= 2 * Math.PI;
          drawWheel();

          // Get result
          const winningIndex = Math.floor(((2 * Math.PI - currentRotation + Math.PI/2) % (2 * Math.PI)) / sliceAngle);
          const resultNumber = (winningIndex + 1);
          document.getElementById("result").innerText = `✨ Your Prediction Number: ${resultNumber}`;
        }
      }
      requestAnimationFrame(animate);
    }

    drawWheel();
  </script>
</body>
</html>
