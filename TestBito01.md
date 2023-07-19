layout: page title: "TestBito01" permalink: /TestBito01

html
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
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.1);
  }
  100% {
    transform: scale(1);
  }
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
 /* New animation style */
@keyframes rotate {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
 /* New balloon style */
.balloon {
  animation: bumb 0.2s infinite alternate, rotate 2s infinite linear;
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
        return colors[Math.floor(Math.random() * colors.length)];
      }
       function updateScore() {
        scoreContainer.textContent = score;
      }
       setInterval(createBalloon, 1000);
       function playPopSound() {
        const sound = new Audio('https://example.com/pop.wav'); // Replace with your sound resource URL
        sound.play();
      }
       document.addEventListener('mouseover', (event) => {
        if (event.target.classList.contains('balloon')) {
          playPopSound();
        }
      });
});
</script>
</body>
</html>
