let circle = {
  x: 100,
  y: 100,
  radius: 30,
  dx: 3,
  dy: 3
};

let rectObj = {
  x: 300,
  y: 300,
  width: 100,
  height: 50,
  dx: -3,
  dy: -3
};

function setup() {
  createCanvas(800, 600);
}

function draw() {
  background(255);

  circle.x += circle.dx;
  circle.y += circle.dy;

  rectObj.x += rectObj.dx;
  rectObj.y += rectObj.dy;

  if (circle.x - circle.radius < 0 || circle.x + circle.radius > width) {
    circle.dx *= -1;
  }
  if (circle.y - circle.radius < 0 || circle.y + circle.radius > height) {
    circle.dy *= -1;
  }

  if (rectObj.x < 0 || rectObj.x + rectObj.width > width) {
    rectObj.dx *= -1;
  }
  if (rectObj.y < 0 || rectObj.y + rectObj.height > height) {
    rectObj.dy *= -1;
  }

  if (detectCollision(circle, rectObj)) {
    circle.dx *= -1;
    circle.dy *= -1;
    rectObj.dx *= -1;
    rectObj.dy *= -1;
  }

  fill(0, 128, 255);
  ellipse(circle.x, circle.y, circle.radius * 2);
  fill(255, 0, 0);
  rect(rectObj.x, rectObj.y, rectObj.width, rectObj.height);
}

function detectCollision(circle, rectObj) {
  let closestX = constrain(circle.x, rectObj.x, rectObj.x + rectObj.width);
  let closestY = constrain(circle.y, rectObj.y, rectObj.y + rectObj.height);
  
  let distance = dist(circle.x, circle.y, closestX, closestY);
  return distance <= circle.radius;
}

function keyPressed() {
  if (key === 'R' || key === 'r') {
    circle.x = 100;
    circle.y = 100;
    circle.dx = 3;
    circle.dy = 3;
    
    rectObj.x = 300;
    rectObj.y = 300;
    rectObj.dx = -3;
    rectObj.dy = -3;
  }
}
