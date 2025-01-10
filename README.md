<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>С Днём Рождения!</title>
  <style>
    /* Общий стиль */
    body {
      margin: 0;
      padding: 0;
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

    /* Анимация всплывающих сердечек */
    .heart {
      position: absolute;
      width: 20px;
      height: 20px;
      background: #ff6b81;
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

    /* Галерея */
    .gallery {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 10px;
      margin: 20px;
    }

    .gallery img {
      width: 150px;
      height: 150px;
      border: 5px solid #f4c17b;
      border-radius: 10px;
      transition: transform 0.3s ease;
    }

    .gallery img:hover {
      transform: scale(1.1);
    }

    /* Кнопка-сюрприз */
    .surprise-btn {
      background: #f4c17b;
      color: #6b4226;
      padding: 15px 30px;
      font-size: 1.2rem;
      border: none;
      border-radius: 30px;
      box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
      cursor: pointer;
      transition: background 0.3s ease, transform 0.2s ease;
    }

    .surprise-btn:hover {
      background: #e5ab65;
      transform: scale(1.1);
    }

    /* Мини-игра */
    .game {
      margin: 20px auto;
      display: none;
      flex-direction: column;
      align-items: center;
    }

    .game .guess-btn {
      background: #ffd966;
      color: #6b4226;
      padding: 10px 20px;
      font-size: 1rem;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      margin-top: 10px;
    }

    .confetti {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      z-index: 1000;
      pointer-events: none;
      display: none;
    }

    .confetti div {
      width: 10px;
      height: 10px;
      background: gold;
      position: absolute;
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
  </style>
</head>
<body>
  <audio autoplay loop>
    <source src="background-music.mp3" type="audio/mp3">
    Ваш браузер не поддерживает музыку.
  </audio>

  <!-- Главная страница -->
  <h1>С Днём Рождения, дорогая тётя!</h1>
  <p>Желаю тебе море радости, счастья, вдохновения и тепла! Пусть этот день будет особенным и наполненным улыбками!</p>

  <!-- Сердечки -->
  <div id="hearts"></div>

  <!-- Фотогалерея -->
  <h2>Фотогалерея</h2>
  <div class="gallery">
    <img src="photo1.jpg" alt="Фото 1">
    <img src="photo2.jpg" alt="Фото 2">
    <img src="photo3.jpg" alt="Фото 3">
  </div>

  <!-- Кнопка-сюрприз -->
  <button class="surprise-btn" onclick="showSurprise()">Нажми на меня</button>
  <div class="confetti" id="confetti"></div>

  <!-- Мини-игра -->
  <div class="game" id="game">
    <h2>Угадай число от 1 до 10</h2>
    <input type="number" id="guess" placeholder="Введите число">
    <button class="guess-btn" onclick="checkGuess()">Угадать</button>
    <p id="game-message"></p>
  </div>

  <script>
    // Анимация сердечек
    function createHeart() {
      const heart = document.createElement('div');
      heart.classList.add('heart');
      heart.style.left = `${Math.random() * 100}%`;
      document.body.appendChild(heart);
      setTimeout(() => heart.remove(), 4000);
    }
    setInterval(createHeart, 500);

    // Конфетти
    function showSurprise() {
      const confetti = document.getElementById('confetti');
      confetti.style.display = 'block';
      for (let i = 0; i < 100; i++) {
        const piece = document.createElement('div');
        piece.style.left = `${Math.random() * 100}vw`;
        piece.style.top = `${Math.random() * -100}vh`;
        piece.style.animationDuration = `${Math.random() * 5 + 2}s`;
        confetti.appendChild(piece);
      }
      setTimeout(() => confetti.style.display = 'none', 5000);
      document.getElementById('game').style.display = 'flex';
    }

    // Мини-игра
    const randomNumber = Math.floor(Math.random() * 10) + 1;
    function checkGuess() {
      const guess = document.getElementById('guess').value;
      const message = document.getElementById('game-message');
      if (guess == randomNumber) {
        message.textContent = 'Угадали! Поздравляем!';
      } else {
        message.textContent = 'Не угадали, попробуйте снова!';
      }
    }
  </script>
</body>
</html>
