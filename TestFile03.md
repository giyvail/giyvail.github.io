layout: page
title: "TestFile03"
permalink: /TestFile03

<!DOCTYPE html>
<html>
<head>
  <title>Balloon Game</title>
  <style>
    #game-container {
      position: relative;
      width: 1000px;
      height: 1000px;
      border: 1px solid black;
      overflow: hidden;
    }

    .balloon {
      position: absolute;
      width: 80px;
      height: 80px;
      background: radial-gradient(circle, #FFB3BA, #FF7171);
      border-radius: 50%;
      cursor: pointer;
      animation: bumb 0.2s infinite alternate;
      transform-origin: center;
      overflow: hidden;
    }

    @keyframes bumb {
      0% { transform: scale(1); }
      50% { transform: scale(1.1); }
      100% { transform: scale(1); }
    }

    .balloon::before {
      content: "";
      position: absolute;
      top: 50%;
      left: 0;
      width: 100%;
      height: 2px;
      background-color: #000;
      border-radius: 50%;
      transform: translateY(-50%);
    }

    .score-container {
      position: fixed;
      top: 0;
      left: 50%;
      transform: translateX(-50%);
      width: 200px;
      height: 100px;
      background-color: rgba(0, 0, 0, 0.5);
      color: #fff;
      font-size: 64px;
      display: flex;
      justify-content: center;
      align-items: center;
    }
  </style>
</head>
<body>
  <div id="game-container"></div>
  <div class="score-container" id="score-container">0</div>

  <script>
    document.addEventListener('DOMContentLoaded', () => {
      const gameContainer = document.getElementById('game-container');
      const scoreContainer = document.getElementById('score-container');
      let score = 0;

      function createBalloon() {
        const balloon = document.createElement('div');
        balloon.className = 'balloon';
        balloon.style.top = '1000px';
        balloon.style.left = `${getRandomPosition()}px`;
        balloon.style.backgroundColor = getRandomColor();

        balloon.addEventListener('mouseover', () => {
          balloon.style.display = 'none';
          score++;
          updateScore();
        });

        gameContainer.appendChild(balloon);

        const flyInterval = setInterval(() => {
          const currentTop = parseInt(balloon.style.top);
          if (currentTop <= 0) {
            clearInterval(flyInterval);
            balloon.remove();
            updateScore();
          } else {
            balloon.style.top = `${currentTop - getRandomSpeed()}px`;
          }
        }, 20);
      }

      function getRandomPosition() {
        return Math.floor(Math.random() * (gameContainer.offsetWidth - 80));
      }

      function getRandomSpeed() {
        return Math.floor(Math.random() * 5) + 1;
      }

      function getRandomColor() {
        const colors = ['#FFB3BA', '#FF7171', '#FFFFBA', '#A0C8FF', '#C8A0FF', '#BAFFBA'];
        return colors[Math.floor(Math.random() * colors.length)];
      }

      function updateScore() {
        scoreContainer.textContent = score;
      }

      setInterval(createBalloon, 1000);
    });
  </script>
</body>
</html>

