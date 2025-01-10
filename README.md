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

    /* Фотогалерея в виде слайд-шоу */
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
      width: 100%;
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

    .dots {
      text-align: center;
      margin-top: 10px;
    }

    .dot {
      cursor: pointer;
      height: 15px;
      width: 15px;
      margin: 0 5px;
      background-color: #bbb;
      border-radius: 50%;
      display: inline-block;
      transition: background-color 0.3s ease;
    }

    .active, .dot:hover {
      background-color: #6b4226;
    }

    /* Мини-игра (пазл) */
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
      background-color: #f4c17b;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 1.5rem;
      color: #6b4226;
      cursor: pointer;
      border-radius: 5px;
      user-select: none;
    }

    .puzzle-piece.correct {
      background-color: #ffd966;
      pointer-events: none;
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
  <p>Пусть этот день будет полон радости, тепла и счастья. Мы всегда рядом, даже если нас разделяют километры. Ты невероятная! Пусть жизнь будет такой же прекрасной, как ты!</p>

  <!-- Слайд-шоу -->
  <div class="slideshow-container">
    <div class="slide">
      <img src="photo1.jpg" alt="Фото 1">
    </div>
    <div class="slide">
      <img src="photo2.jpg" alt="Фото 2">
    </div>
    <div class="slide">
      <img src="photo3.jpg" alt="Фото 3">
    </div>
    <div class="slide">
      <img src="photo4.jpg" alt="Фото 4">
    </div>
    <div class="slide">
      <img src="photo5.jpg" alt="Фото 5">
    </div>
    <div class="slide">
      <img src="photo6.jpg" alt="Фото 6">
    </div>
    <div class="slide">
      <img src="photo7.jpg" alt="Фото 7">
    </div>
    <div class="slide">
      <img src="photo8.jpg" alt="Фото 8">
    </div>
    <div class="slide">
      <img src="photo9.jpg" alt="Фото 9">
    </div>
    <div class="slide">
      <img src="photo10.jpg" alt="Фото 10">
    </div>
    <div class="slide">
      <img src="photo11.jpg" alt="Фото 11">
    </div>
    <div class="slide">
      <img src="photo12.jpg" alt="Фото 12">
    </div>

    <button class="prev" onclick="changeSlide(-1)">&#10094;</button>
    <button class="next" onclick="changeSlide(1)">&#10095;</button>
  </div>

  <div class="dots" id="dots"></div>

  <!-- Мини-игра -->
  <div class="puzzle-container">
    <h2>Собери пазл</h2>
    <p>Нажми на блоки, чтобы собрать правильный порядок (1-9).</p>
    <div class="puzzle" id="puzzle"></div>
    <p id="puzzle-message"></p>
  </div>

  <script>
    // Слайд-шоу
    let slideIndex = 0;
    showSlides();

    function showSlides() {
      const slides = document.querySelectorAll('.slide');
      const dots = document.querySelector('#dots');
      slides.forEach((slide, index) => slide.style.display = index === slideIndex ? 'block' : 'none');

      dots.innerHTML = '';
      slides.forEach((_, index) => {
        const dot = document.createElement('span');
        dot.className = `dot ${index === slideIndex ? 'active' : ''}`;
        dot.onclick = () => setSlide(index);
        dots.appendChild(dot);
      });
    }

    function changeSlide(n) {
      slideIndex = (slideIndex + n + 12) % 12;
      showSlides();
    }

    function setSlide(n) {
      slideIndex = n;
      showSlides();
    }

    // Мини-игра (пазл)
    const puzzle = document.getElementById('puzzle');
    const pieces = Array.from({ length: 9 }, (_, i) => i + 1);
    let shuffled = [...pieces].sort(() => Math.random() - 0.5);

    function renderPuzzle() {
      puzzle.innerHTML = '';
      shuffled.forEach((num, index) => {
        const piece = document.createElement('div');
        piece.className = `puzzle-piece ${num === index + 1 ? 'correct' : ''}`;
        piece.textContent = num;
        piece.onclick = () => movePiece(index);
        puzzle.appendChild(piece);
      });

      if (shuffled.every((num, index) => num === index + 1)) {
        document.getElementById('puzzle-message').textContent = 'Поздравляю! Пазл собран!';
      }
    }

    function movePiece(index) {
      if (index > 0 && shuffled[index - 1] === 9) {
        [shuffled[index], shuffled[index - 1]] = [shuffled[index - 1], shuffled[index]];
      } else if (index < 8 && shuffled[index + 1] === 9) {
        [shuffled[index], shuffled[index + 1]] = [shuffled[index + 1], shuffled[index]];
      }
      renderPuzzle();
    }

    renderPuzzle();
  </script>
</body>
</html>
