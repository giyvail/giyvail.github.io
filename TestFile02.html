layout: page
title: "TestFile02"
permalink: /TestFile02

<!DOCTYPE html>
<html>
<head>
  <title>Balloon Game</title>
  <style>
    #game-container {
      position: relative;
      width: 2560px;
      height: 1440px;
      border: 1px solid black;
      overflow: hidden;
    }

    .balloon {
      position: absolute;
      width: 100px;
      height: 160px;
      background-image: url('balloon-texture.png');
      background-size: cover;
      cursor: pointer;
      animation: bumb 0.2s infinite alternate;
    }

    @keyframes bumb {
      0% { transform: scale(1); }
      50% { transform: scale(1.1); }
      100% { transform: scale(1); }
    }
  </style>
</head>
<body>
  <div id="game-container"></div>

  <script>
    document.addEventListener('DOMContentLoaded', () => {
      const gameContainer = document.getElementById('game-container');
      let score = 0;

      function createBalloon() {
        const balloon = document.createElement('div');
        balloon.className = 'balloon';
        balloon.style.top = '1440px';
        balloon.style.left = `${getRandomPosition()}px`;

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
        return Math.floor(Math.random() * (gameContainer.offsetWidth - 100));
      }

      function getRandomSpeed() {
        return Math.floor(Math.random() * 5) + 1;
      }

      function updateScore() {
        document.getElementById('score').textContent = `Score: ${score}`;
      }

      setInterval(createBalloon, 1000);
    });
  </script>
</body>
</html>


