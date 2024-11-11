class Circle {
  constructor(x, y, radius, dx, dy) {
    this.x = x;
    this.y = y;
    this.radius = radius;
    this.dx = dx;
    this.dy = dy;
  }

  update() {
    this.x += this.dx;
    this.y += this.dy;
    this.checkBounds();
  }

  checkBounds() {
    if (this.x - this.radius < 0 || this.x + this.radius > width) {
      this.dx *= -1;
    }
    if (this.y - this.radius < 0 || this.y + this.radius > height) {
      this.dy *= -1;
    }
  }

  display() {
    fill(0, 128, 255);
    ellipse(this.x, this.y, this.radius * 2);
  }
}

class Rectangle {
  constructor(x, y, width, height, dx, dy) {
    this.x = x;
    this.y = y;
    this.width = width;
    this.height = height;
    this.dx = dx;
    this.dy = dy;
  }

  update() {
    this.x += this.dx;
    this.y += this.dy;
    this.checkBounds();
  }

  checkBounds() {
    if (this.x < 0 || this.x + this.width > width) {
      this.dx *= -1;
    }
    if (this.y < 0 || this.y + this.height > height) {
      this.dy *= -1;
    }
  }

  display() {
    fill(255, 0, 0);
    rect(this.x, this.y, this.width, this.height);
  }
}

let circle;
let rectObj;

function setup() {
  createCanvas(800, 600);
  circle = new Circle(100, 100, 30, 3, 3);
  rectObj = new Rectangle(300, 300, 100, 50, -3, -3);
}

function draw() {
  background(255);
  circle.update();
  circle.display();
  rectObj.update();
  rectObj.display();

  if (detectCollision(circle, rectObj)) {
    circle.dx *= -1;
    circle.dy *= -1;
    rectObj.dx *= -1;
    rectObj.dy *= -1;
  }
}

function detectCollision(circle, rectObj) {
  let closestX = constrain(circle.x, rectObj.x, rectObj.x + rectObj.width);
  let closestY = constrain(circle.y, rectObj.y, rectObj.y + rectObj.height);
  let distance = dist(circle.x, circle.y, closestX, closestY);
  return distance <= circle.radius;
}

function keyPressed() {
  if (key === 'R' || key === 'r') {
    circle = new Circle(100, 100, 30, 3, 3);
    rectObj = new Rectangle(300, 300, 100, 50, -3, -3);
  }
}


Classes (Circle and Rectangle): Encapsulate the properties and methods related to each shape.
setup(): Initializes the circle and rectObj as instances of their respective classes.
draw(): Updates and displays both shapes and checks for collisions.
detectCollision(): Checks for collision between the circle and rectangle and returns true if they collide.
keyPressed(): Resets the position and speed of both shapes when the 'R' key is pressed.
