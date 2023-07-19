layout: page
title: "TestFile01"
permalink: /TestFile01

<!DOCTYPE html>
<html>
<head>
<title>Balloon Game</title>
<style>
body {
  background-color: #ffffff;
}

.balloon {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  background-color: red;
  position: absolute;
  top: 0px;
  left: 0px;
  animation: move 2s linear infinite;
}

@keyframes move {
  0% {
    top: 0px;
    left: 0px;
  }
  100% {
    top: 100vh;
    left: 100vw;
  }
}

</style>
</head>
<body>
<script>
var balloons = [];

for (var i = 0; i < 10; i++) {
  balloons.push({
    x: Math.random() * window.innerWidth,
    y: 0,
    width: 50,
    height: 50,
    color: Math.floor(Math.random() * 100) + 1
  });
}

var mouseX = 0;
var mouseY = 0;

window.addEventListener('mousemove', function(event) {
  mouseX = event.clientX;
  mouseY = event.clientY;
});

function update() {
  for (var i = 0; i < balloons.length; i++) {
    balloons[i].y += 5;

    if (balloons[i].y > window.innerHeight) {
      balloons[i].y = 0;
    }

    if (balloons[i].x > mouseX - balloons[i].width / 2 && balloons[i].x < mouseX + balloons[i].width / 2 &&
      balloons[i].y > mouseY - balloons[i].height / 2 && balloons[i].y < mouseY + balloons[i].height / 2) {
      balloons[i].color = Math.floor(Math.random() * 100) + 1;
    }
  }
}

setInterval(update, 20);

for (var i = 0; i < balloons.length; i++) {
  var balloon = document.createElement('div');
  balloon.className = 'balloon';
  balloon.style.width = balloons[i].width + 'px';
  balloon.style.height = balloons[i].height + 'px';
  balloon.style.background = 'rgb(' + balloons[i].color + ', 0, 0)';
  document.body.appendChild(balloon);
}
</script>
</body>
</html>