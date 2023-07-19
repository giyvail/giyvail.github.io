layout: page
title: "TestFile01"
permalink: /TestFile01

<!DOCTYPE html>
<html>
<head>
  <title>Balloon Game</title>
  <style>
    #game-container {
      position: relative;
      width: 400px;
      height: 500px;
      border: 1px solid black;
      overflow: hidden;
    }

    .balloon {
      position: absolute;
      width: 40px;
      height: 40px;
      border-radius: 50%;
      cursor: pointer;
    }

    .red { background-color: red; }
    .blue { background-color: blue; }
    .green { background-color: green; }
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
        balloon.className = `balloon ${getRandomColor()}`;
        balloon.style.top = '500px';
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

      function getRandomColor() {
        const colors = ['red', 'blue', 'green'];
        return colors[Math.floor(Math.random() * colors.length)];
      }

      function getRandomPosition() {
        return Math.floor(Math.random() * (gameContainer.offsetWidth - 40));
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


