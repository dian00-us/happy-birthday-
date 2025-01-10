<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>С Днём Рождения!</title>
  <style>
    /* Основной стиль */
    body {
      margin: 0;
      font-family: 'Dancing Script', cursive, 'Arial', sans-serif;
      background: linear-gradient(to bottom, #fff8e7, #ffe5b4);
      color: #6b4226;
      text-align: center;
      overflow-x: hidden;
    }

    h1 {
      font-size: 3rem;
      margin: 20px 0;
      text-shadow: 2px 2px 5px rgba(0, 0, 0, 0.3);
    }

    p {
      font-size: 1.2rem;
      margin: 10px 0;
    }

    /* Фотогалерея */
    .slideshow-container {
      max-width: 80%;
      margin: 20px auto;
      position: relative;
      overflow: hidden;
      border: 10px solid #f4c17b;
      border-radius: 15px;
      box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
    }

    .slide {
      display: none;
    }

    .slide img {
      width: 100%;
      border-radius: 15px;
    }

    .prev, .next {
      cursor: pointer;
      position: absolute;
      top: 50%;
      transform: translateY(-50%);
      padding: 15px;
      background-color: rgba(0, 0, 0, 0.5);
      color: #fff;
      font-size: 20px;
      border: none;
      border-radius: 50%;
    }

    .prev {
      left: 10px;
    }

    .next {
      right: 10px;
    }

    /* Пазл */
    .puzzle-container {
      margin: 30px auto;
      max-width: 400px;
    }

    .puzzle {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 5px;
    }

    .puzzle-piece {
      width: 100%;
      height: 100px;
      background-size: 300px 300px;
      cursor: pointer;
      border-radius: 5px;
      user-select: none;
    }

    .puzzle-piece.correct {
      pointer-events: none;
      box-shadow: 0 0 5px 2px #ffd966;
    }

    /* Конфетти */
    .confetti {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
    }

    .confetti div {
      position: absolute;
      width: 10px;
      height: 10px;
      background-color: gold;
      animation: fall 5s linear infinite;
    }

    @keyframes fall {
      0% {
        transform: translateY(-100%);
      }
      100% {
        transform: translateY(100vh) rotate(360deg);
      }
    }

    /* Всплывающие сердечки */
    .heart {
      position: absolute;
      width: 20px;
      height: 20px;
      background: red;
      clip-path: polygon(50% 0%, 100% 35%, 75% 100%, 50% 75%, 25% 100%, 0% 35%);
      animation: floatUp 4s ease-in-out infinite;
    }

    @keyframes floatUp {
      0% {
        opacity: 1;
        transform: translateY(0) scale(1);
      }
      100% {
        opacity: 0;
        transform: translateY(-200px) scale(1.5);
      }
    }
  </style>
</head>
<body>
  <audio autoplay loop>
    <source src="background-music.mp3" type="audio/mp3">
    Ваш браузер не поддерживает музыку.
  </audio>

  <!-- Главная страница -->
  <h1>С Днём Рождения, дорогая тётя!</h1>
  <p>Ты - невероятная! Пусть в твоей жизни будет больше счастья, радости и чудес! Мы всегда рядом!</p>

  <!-- Фотогалерея -->
  <div class="slideshow-container">
    <div class="slide">
      <img src="photo1.jpg" alt="Фото 1">
    </div>
    <div class="slide">
      <img src="photo2.jpg" alt="Фото 2">
    </div>
    <!-- Добавьте ещё 10 фото сюда -->
    <button class="prev" onclick="changeSlide(-1)">&#10094;</button>
    <button class="next" onclick="changeSlide(1)">&#10095;</button>
  </div>

  <!-- Пазл -->
  <div class="puzzle-container">
    <h2>Собери пазл</h2>
    <p>Нажми на блоки, чтобы собрать фотографию!</p>
    <div class="puzzle" id="puzzle"></div>
    <p id="puzzle-message"></p>
  </div>

  <div class="confetti" id="confetti"></div>
  <script>
    // Конфетти
    function showConfetti() {
      const confetti = document.getElementById('confetti');
      for (let i = 0; i < 100; i++) {
        const piece = document.createElement('div');
        piece.style.left = `${Math.random() * 100}vw`;
        piece.style.top = `${Math.random() * -100}vh`;
        piece.style.animationDuration = `${Math.random() * 5 + 2}s`;
        confetti.appendChild(piece);
      }
    }
    showConfetti();

    // Всплывающие сердечки
    function createHeart() {
      const heart = document.createElement('div');
      heart.classList.add('heart');
      heart.style.left = `${Math.random() * 100}%`;
      document.body.appendChild(heart);
      setTimeout(() => heart.remove(), 4000);
    }
    setInterval(createHeart, 500);

    // Пазл
    const puzzle = document.getElementById('puzzle');
    const image = 'photo1.jpg'; // Укажите путь к фото
    const pieces = Array.from({ length: 9 }, (_, i) => i);
    let shuffled = [...pieces].sort(() => Math.random() - 0.5);

    function renderPuzzle() {
      puzzle.innerHTML = '';
      shuffled.forEach((num, index) => {
        const piece = document.createElement('div');
        piece.className = `puzzle-piece ${num === index ? 'correct' : ''}`;
        piece.style.backgroundImage = `url(${image})`;
        piece.style.backgroundPosition = `${(num % 3) * -100}px ${(Math.floor(num / 3)) * -100}px`;
        piece.onclick = () => swapPieces(index);
        puzzle.appendChild(piece);
      });

      if (shuffled.every((num, index) => num === index)) {
        document.getElementById('puzzle-message').textContent = 'Поздравляю! Пазл собран!';
      }
    }

    function swapPieces(index) {
      const emptyIndex = shuffled.indexOf(8); // Последняя пустая часть
      if ([index - 1, index + 1, index - 3, index + 3].includes(emptyIndex)) {
        [shuffled[index], shuffled[emptyIndex]] = [shuffled[emptyIndex], shuffled[index]];
        renderPuzzle();
      }
    }

    renderPuzzle();
  </script>
</body>
</html>
