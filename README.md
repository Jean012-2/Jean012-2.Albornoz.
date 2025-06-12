<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Familia Albornoz</title>
  <style>
    html, body {
      margin: 0;
      padding: 0;
      overflow: hidden;
      height: 100%;
      background-color: black;
      color: white;
      font-family: 'Arial', sans-serif;
    }

    #overlay {
      position: absolute;
      top: 0;
      left: 0;
      z-index: 1;
      width: 100%;
      height: 100%;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      text-align: center;
      pointer-events: none;
    }

    h1 {
      font-size: 4em;
      margin-bottom: 20px;
    }

    ul {
      list-style: none;
      padding: 0;
      font-size: 1.2em;
    }

    li {
      margin: 5px 0;
    }

    canvas {
      position: absolute;
      top: 0;
      left: 0;
      z-index: 0;
    }
  </style>
</head>
<body>
  <canvas id="stars"></canvas>
  <div id="overlay">
    <h1>Familia Albornoz</h1>
    <ul>
      <li>Pablo Albornoz Martínez</li>
      <li>Jean Pablo Albornoz Tacuchi</li>
      <li>Hubel Albornoz Tacuchi</li>
      <li>Ana Cristina Albornoz Tacuchi</li>
      <li>Nelinda Albornoz Tacuchi</li>
      <li>Francisco Albornoz Tacuchi</li>
      <li>Lucio Albornoz</li>
      <li>Suly Albornoz Reyes</li>
      <li>Jhen Baltazar Albornoz</li>
      <li>Briana Albornoz Reyes</li>
      <li>Eyal Baltazar Albornoz</li>
      <li>Alexa Albornoz Reyes</li>
      <li>Keysi Adriani Albornoz Arias</li>
    </ul>
  </div>

  <script>
    const canvas = document.getElementById('stars');
    const ctx = canvas.getContext('2d');
    let particles = [];

    function resizeCanvas() {
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    }

    window.addEventListener('resize', resizeCanvas);
    resizeCanvas();

    function createExplosion(x, y) {
      for (let i = 0; i < 100; i++) {
        particles.push({
          x: x,
          y: y,
          vx: (Math.random() - 0.5) * 4,
          vy: (Math.random() - 0.5) * 4,
          life: 100,
          color: `hsl(${Math.random() * 360}, 100%, 70%)`
        });
      }
    }

    function update() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      particles = particles.filter(p => p.life > 0);

      for (let p of particles) {
        ctx.beginPath();
        ctx.arc(p.x, p.y, 2, 0, Math.PI * 2);
        ctx.fillStyle = p.color;
        ctx.fill();
        p.x += p.vx;
        p.y += p.vy;
        p.life--;
      }

      requestAnimationFrame(update);
    }

    setInterval(() => {
      const x = Math.random() * canvas.width;
      const y = Math.random() * canvas.height;
      createExplosion(x, y);
    }, 500);

    update();
  </script>
</body>
</html>
