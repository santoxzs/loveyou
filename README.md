<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Para Minha Criança ❤️</title>
  <link href="https://fonts.googleapis.com/css2?family=Montserrat&display=swap" rel="stylesheet">
  <style>
    html, body {
      margin: 0;
      padding: 0;
      height: 100%;
      background: #b22222;
      overflow: hidden;
      font-family: 'Montserrat', sans-serif;
    }

    canvas {
      position: fixed;
      top: 0;
      left: 0;
      z-index: -1;
    }

    .container {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      background: rgba(255, 255, 255, 0.1);
      backdrop-filter: blur(10px);
      padding: 30px;
      border-radius: 20px;
      text-align: center;
      animation: fadeIn 2s ease forwards;
      opacity: 0;
      max-width: 90%;
    }

    .polaroid {
      background: white;
      padding: 10px;
      border-radius: 10px;
      box-shadow: 0 5px 15px rgba(0,0,0,0.3);
      margin-bottom: 20px;
    }

    .polaroid img {
      width: 100%;
      max-width: 350px;
      border-radius: 5px;
      cursor: pointer;
      animation: pulse 3s infinite;
    }

    .caption {
      font-size: 1.2em;
      margin-top: 10px;
      color: #b22222;
    }

    .text-below {
      color: black;
      font-size: 1.4em;
      text-shadow: 1px 1px 3px rgba(255,255,255,0.3);
      max-width: 500px;
      margin: 0 auto;
    }

    .music-player {
      margin-top: 20px;
    }

    @keyframes fadeIn {
      to { opacity: 1; }
    }

    @keyframes pulse {
      0%, 100% { transform: scale(1); }
      50% { transform: scale(1.03); }
    }
  </style>
</head>
<body>
  <canvas id="heartCanvas"></canvas>

  <div class="container">
    <div class="polaroid">
      <img id="mainImage" src="https://i.postimg.cc/HVxrX9W2/foto-pb.jpg" alt="Casal"/>
      <div class="caption">Clique na foto e veja a mágica ✨</div>
    </div>
    <div class="text-below">
      você na minha vida é tão especial assim como o impala é especial para o Dean, você chegou na minha vida e a mudou por completo, meus dias passaram a ter mais cor e a minha vida passou a ser mais feliz, não pude comprar um presente mas fiz isso para você. saiba que eu te amo muito meu amor da minha vida 🩷✨️
    </div>
    <div class="music-player">
      <audio controls>
        <source src="https://cdn.pixabay.com/audio/2023/08/06/audio_0ec5f030b3.mp3" type="audio/mpeg">
        Seu navegador não suporta o áudio.
      </audio>
      <p style="color: white; margin-top: 8px;">Trecho: "Cause it's too cold... for you here..."</p>
    </div>
  </div>

  <script>
    const canvas = document.getElementById('heartCanvas');
    const ctx = canvas.getContext('2d');
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;

    window.addEventListener('resize', () => {
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    });

    const hearts = [];

    function createHeart() {
      return {
        x: Math.random() * canvas.width,
        y: -20,
        size: Math.random() * 1.5 + 1,
        speed: Math.random() * 1.5 + 1,
        opacity: Math.random() * 0.5 + 0.5
      };
    }

    function drawHeart(heart) {
      ctx.save();
      ctx.translate(heart.x, heart.y);
      ctx.scale(heart.size, heart.size);
      ctx.beginPath();
      ctx.moveTo(0, 0);
      ctx.bezierCurveTo(0, -3, -3, -3, -3, 0);
      ctx.bezierCurveTo(-3, 3, 0, 5, 0, 6);
      ctx.bezierCurveTo(0, 5, 3, 3, 3, 0);
      ctx.bezierCurveTo(3, -3, 0, -3, 0, 0);
      ctx.closePath();
      ctx.fillStyle = `rgba(255, 192, 203, ${heart.opacity})`;
      ctx.shadowColor = 'pink';
      ctx.shadowBlur = 10;
      ctx.fill();
      ctx.restore();
    }

    function animate() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);

      // Adiciona novos corações constantemente
      if (hearts.length < 200) {
        hearts.push(createHeart());
      }

      hearts.forEach((heart, index) => {
        heart.y += heart.speed;
        drawHeart(heart);
        if (heart.y > canvas.height + 20) {
          hearts.splice(index, 1);
        }
      });

      requestAnimationFrame(animate);
    }

    document.getElementById('mainImage').addEventListener('click', () => {
      const img = document.getElementById('mainImage');
      img.src = 'https://i.postimg.cc/s11zJ6Sv/foto-colorida.jpg';
    });

    window.onload = () => {
      animate();
    };
  </script>
</body>
</html>
