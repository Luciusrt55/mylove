<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Carta Interactiva para Andrea Carolina</title>
  <!-- Fuente romántica desde Google Fonts -->
  <link href="https://fonts.googleapis.com/css2?family=Indie+Flower&display=swap" rel="stylesheet">
  <style>
    /* Fondo romántico en tonos pastel rosa */
    body {
      margin: 0;
      padding: 0;
      height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      background: linear-gradient(135deg, #ffc1cc, #ffe4e1);
      font-family: 'Indie Flower', cursive;
    }
    /* Contenedor con perspectiva para el efecto 3D */
    .card-container {
      perspective: 1200px;
      cursor: pointer;
      position: relative;
    }
    /* Carta horizontal */
    .card {
      width: 500px;
      height: 300px;
      position: relative;
      transform-style: preserve-3d;
      transition: transform 1s;
    }
    .card.flipped {
      transform: rotateY(180deg);
    }
    .card-face {
      position: absolute;
      width: 100%;
      height: 100%;
      backface-visibility: hidden;
      border-radius: 10px;
      box-shadow: 0 8px 20px rgba(0,0,0,0.2);
    }
    /* Parte frontal: sobre elegante horizontal */
    .card-front {
      background: #fff;
      border: 2px solid #ff8fad;
      position: relative;
      display: flex;
      justify-content: center;
      align-items: center;
    }
    /* Solapa del sobre, con un toque elegante */
    .card-front::before {
      content: "";
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 40%;
      background: #ff8fad;
      clip-path: polygon(0 0, 100% 0, 85% 100%, 15% 100%);
    }
    .card-front h2 {
      position: relative;
      color: #ff8fad;
      font-size: 2.5rem;
      margin: 0;
    }
    /* Parte trasera: hoja de oficio */
    .card-back {
      background: #fff;
      transform: rotateY(180deg);
      padding: 20px 30px;
      box-sizing: border-box;
      background-image: repeating-linear-gradient(
        0deg,
        transparent,
        transparent 28px,
        rgba(0,0,0,0.05) 29px,
        rgba(0,0,0,0.05) 30px
      );
      position: relative;
      overflow: hidden; /* Contiene los elementos flotantes */
    }
    .card-back p {
      font-size: 1.3rem;
      line-height: 1.6;
      color: #333;
      margin: 0;
    }
    /* Estilo para los elementos flotantes (flores y corazones) */
    .floating {
      position: absolute;
      font-size: 2rem;
      opacity: 0.9;
      animation: floatUp 3s linear forwards;
      pointer-events: none;
    }
    @keyframes floatUp {
      0% { transform: translateY(0) rotate(0deg); opacity: 1; }
      100% { transform: translateY(-150px) rotate(360deg); opacity: 0; }
    }
  </style>
</head>
<body>
  <!-- Al hacer clic en el contenedor se activa el flip de la carta -->
  <div class="card-container" onclick="flipCard()">
    <div class="card" id="card">
      <!-- Parte frontal: el sobre elegante en formato horizontal -->
      <div class="card-face card-front">
        <h2>Para 💗Andrea Carolina💗</h2>
      </div>
      <!-- Parte trasera: la hoja de oficio con el mensaje -->
      <div class="card-face card-back" id="cardBack">
        <p>
          💕💘Te has convertido en la personita más especial y linda que tengo en mi vida, <br>
          desde que te conozco no he dejado ni un solo momento de pensar en ti, <br>
          me tienes enamorado, demasiado diría yo, <br>
          soy tan feliz de conocerte, mi amor. <br>
          No cambies nunca, mi amor, y sigámonos amando como siempre, mi vida💕💘.
        </p>
      </div>
    </div>
  </div>

  <script>
    const card = document.getElementById('card');
    const cardBack = document.getElementById('cardBack');
    let isFlipped = false;
    
    function flipCard() {
      card.classList.toggle('flipped');
      isFlipped = !isFlipped;
      // Si la carta se abre, inicia los elementos flotantes
      if (isFlipped) {
        startFloatingElements();
      }
    }
    
    function startFloatingElements() {
      // Duración de generación de elementos: 3 segundos, creando uno cada 300 ms
      const floatingDuration = 3000;
      const interval = 300;
      const endTime = Date.now() + floatingDuration;
      const symbols = ["💕", "🌸", "💖", "🌷", "❤️", "💗"];
      
      function createFloating() {
        if (Date.now() > endTime) return;
        
        const floating = document.createElement('div');
        floating.classList.add('floating');
        // Selecciona un símbolo aleatorio (corazón o flor)
        const symbol = symbols[Math.floor(Math.random() * symbols.length)];
        floating.textContent = symbol;
        // Posición aleatoria dentro de la carta (relativa al cardBack)
        const x = Math.random() * (cardBack.clientWidth - 30);
        floating.style.left = x + 'px';
        // Empieza justo en la parte inferior del cardBack
        floating.style.top = cardBack.clientHeight + 'px';
        // Duración de la animación aleatoria entre 2.5 y 3.5 segundos
        floating.style.animationDuration = (Math.random() * 1 + 2.5) + 's';
        cardBack.appendChild(floating);
        // Elimina el elemento tras finalizar la animación
        setTimeout(() => {
          floating.remove();
        }, 3500);
        
        setTimeout(createFloating, interval);
      }
      
      createFloating();
    }
  </script>
</body>
</html>
