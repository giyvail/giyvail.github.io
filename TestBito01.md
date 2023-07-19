layout: page title: "TestBito01" permalink: /TestBito01

<!DOCTYPE html>
<html lang="en">
<head>
  <title>Balloon Game</title>
  <link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/material-design-lite/1.3.0/material.min.css">
  <style>
    .mdl-card {
      display: flex;
      justify-content: center;
      align-items: center;
      text-align: center;
      padding: 16px;
      margin: 16px;
    }
    .mdl-card#game-container {
      width: 400px;
      height: 400px;
      background-color: #b3e5fc;
      overflow: hidden;
    }
    .mdl-card#score-container {
      width: 200px;
      height: 100px;
      background-color: rgba(0, 0, 0, 0.5);
      color: #fff;
      font-size: 64px;
    }
    .mdl-card#score-container i {
      font-size: 48px;
      margin-right: 8px;
    }
    .mdl-card#score-container .score {
      font-size: 64px;
    }
  </style>
</head>
<body>
  <div class="mdl-card" id="game-container"></div>
  <div class="mdl-card mdl-shadow--2dp" id="score-container">
    <i class="material-icons">score</i>
    <span class="score">0</span>
  </div>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/material-design-lite/1.3.0/material.min.js"></script>
  <script>
    document.addEventListener('DOMContentLoaded', () => {
      const gameContainer = document.getElementById('game-container');
      const scoreContainer = document.getElementById('score-container');
      let score = 0;
      const colors = [
        '#FFB3BA',
        '#FF7171',
        '#FFFFBA',
        '#A0C8FF',
        '#C8A0FF',
        '#BAFFBA',
        '#90EE90',
        '#D3D3D3',
        '#228B22',
      ];
      function createBalloon() {
        const balloon = document.createElement('div');
        balloon.className = 'balloon';
        balloon.style.top = '1000px';
        balloon.style.left = `${getRandomPosition()}px`;
        balloon.style.backgroundColor = getRandomColor();
        balloon.style.animationDuration = `${getRandomDuration()}s`;
        balloon.addEventListener('mouseover', () => {
          balloon.style.display = 'none';
          score++;
          updateScore();
          playPopSound();
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
        return Math.floor(Math.random() * 10) + 1;
      }
      function getRandomColor() {
        const gradient = `radial-gradient(circle, ${getRandomGradientColor()}, ${getRandomGradientColor()})`;
        return gradient;
      }
      function getRandomGradientColor() {
        return colors[Math.floor(Math.random() * colors.length)];
      }
      function getRandomDuration() {
        return Math.floor(Math.random() * 5) + 1;
      }
      function updateScore() {
        scoreContainer.querySelector('.score').textContent = score;
      }
      setInterval(createBalloon, 1000);
      function playPopSound() {
        const sound = new Audio('https://example.com/pop.wav'); // Replace with your sound resource URL
        sound.play();
      }
      document.addEventListener('mouseover', (event) => {
        if (event.target.classList.contains('balloon')) {
          event.target.style.animation = 'bumb 0.2s infinite alternate';
          playPopSound();
        }
      });
    });
  </script>
</body>
</html>
