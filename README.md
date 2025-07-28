<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8" />
  <title>Игра: Раскрась звуки</title>
  <style>
    body {
      font-family: sans-serif;
      text-align: center;
      background-color: #f0f0f0;
      padding: 30px;
    }

    .word {
      font-size: 48px;
      margin-bottom: 30px;
      filter: blur(8px);
      cursor: pointer;
      user-select: none;
      transition: filter 0.3s;
      display: inline-block;
    }

    .word.visible {
      filter: none;
    }

    .square-row {
      display: flex;
      justify-content: center;
      margin-top: 20px;
    }

    .square-container {
      position: relative;
      margin: 0 10px;
    }

    .square {
      width: 60px;
      height: 60px;
      background-color: #ddd;
      border: 2px solid #999;
      cursor: pointer;
    }

    .top-square {
      width: 30px;
      height: 30px;
      background-color: transparent;
      position: absolute;
      top: -35px;
      left: 15px;
      border-radius: 50%;
      border: 2px dashed #999;
      cursor: pointer;
    }

    .controls {
      margin-top: 30px;
    }

    .color-button {
      padding: 10px 15px;
      margin: 5px;
      font-size: 16px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      color: #fff;
    }

    .blue { background-color: #007BFF; }
    .red { background-color: #DC3545; }
    .green { background-color: #28A745; }
  </style>
</head>
<body>

  <h2>Игра: Раскрась звуки</h2>
  <p>Нажми на слово, чтобы его показать или скрыть. Выбери цвет, затем кликни по квадрату или кружку. Повторный клик — сброс цвета.</p>

  <div class="word" id="wordDisplay"></div>
  <div class="square-row" id="squareRow"></div>

  <div class="controls">
    <button class="color-button blue" onclick="selectColor('blue')">Синий</button>
    <button class="color-button red" onclick="selectColor('red')">Красный</button>
    <button class="color-button green" onclick="selectColor('green')">Зелёный (сверху)</button>
  </div>

  <script>
    const words = ["кот", "мама", "дом", "мак", "нос", "лес", "мир", "луна"];
    const selectedWord = words[Math.floor(Math.random() * words.length)];
    const wordDisplay = document.getElementById("wordDisplay");
    const squareRow = document.getElementById("squareRow");

    let currentColor = null;

    wordDisplay.textContent = selectedWord;
    wordDisplay.addEventListener("click", () => {
      wordDisplay.classList.toggle("visible");
    });

    for (let i = 0; i < selectedWord.length; i++) {
      const container = document.createElement("div");
      container.className = "square-container";

      const topSquare = document.createElement("div");
      topSquare.className = "top-square";
      topSquare.dataset.index = i;

      const square = document.createElement("div");
      square.className = "square";
      square.dataset.index = i;

      square.addEventListener("click", () => {
        if (!currentColor) {
          square.style.backgroundColor = "#ddd";
        } else {
          const currentBg = square.style.backgroundColor;
          const newColor = currentColor === "blue" ? "rgb(0, 123, 255)" : "rgb(220, 53, 69)";
          square.style.backgroundColor = (currentBg === newColor) ? "#ddd" : newColor;
        }
      });

      topSquare.addEventListener("click", () => {
        if (!currentColor) {
          topSquare.style.backgroundColor = "transparent";
        } else if (currentColor === "green") {
          topSquare.style.backgroundColor =
            (topSquare.style.backgroundColor === "rgb(40, 167, 69)") ? "transparent" : "#28A745";
        }
      });

      container.appendChild(topSquare);
      container.appendChild(square);
      squareRow.appendChild(container);
    }

    function selectColor(color) {
      currentColor = color;
    }
  </script>

</body>
</html>
