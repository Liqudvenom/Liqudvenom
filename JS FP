const canvas = document.getElementById("canvas");
const ctx = canvas.getContext("2d");

canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

const particles = [];

const shapes = ["circle", "square", "triangle", "pentagon", "hexagon", "star"]; // Additional shapes
const colors = [
  "#FF5733",
  "#FFC300",
  "#FF33FF",
  "#33FFDD",
  "#3366FF",
  "#FF3366"
]; // Different colors

class Particle {
  constructor(x, y, radius, shape, color) {
    this.x = x;
    this.y = y;
    this.radius = radius;
    this.shape = shape;
    this.color = color;
    this.velocityX = Math.random() * 2 - 1;
    this.velocityY = Math.random() * 2 - 1;
  }

  draw() {
    ctx.beginPath();
    if (this.shape === "circle") {
      ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2);
    } else if (this.shape === "square") {
      ctx.rect(
        this.x - this.radius,
        this.y - this.radius,
        this.radius * 2,
        this.radius * 2
      );
    } else if (this.shape === "triangle") {
      ctx.moveTo(this.x, this.y - this.radius);
      ctx.lineTo(this.x + this.radius, this.y + this.radius);
      ctx.lineTo(this.x - this.radius, this.y + this.radius);
      ctx.closePath();
    } else if (this.shape === "pentagon") {
      const angle = (Math.PI * 2) / 5;
      ctx.moveTo(
        this.x + this.radius * Math.cos(0),
        this.y + this.radius * Math.sin(0)
      );
      for (let i = 1; i < 5; i++) {
        ctx.lineTo(
          this.x + this.radius * Math.cos(angle * i),
          this.y + this.radius * Math.sin(angle * i)
        );
      }
      ctx.closePath();
    } else if (this.shape === "hexagon") {
      const angle = (Math.PI * 2) / 6;
      ctx.moveTo(
        this.x + this.radius * Math.cos(0),
        this.y + this.radius * Math.sin(0)
      );
      for (let i = 1; i < 6; i++) {
        ctx.lineTo(
          this.x + this.radius * Math.cos(angle * i),
          this.y + this.radius * Math.sin(angle * i)
        );
      }
      ctx.closePath();
    } else if (this.shape === "star") {
      const angle = (Math.PI * 2) / 10;
      ctx.moveTo(
        this.x + this.radius * Math.cos(0),
        this.y + this.radius * Math.sin(0)
      );
      for (let i = 1; i < 10; i++) {
        const r = i % 2 === 0 ? this.radius * 0.5 : this.radius;
        ctx.lineTo(
          this.x + r * Math.cos(angle * i),
          this.y + r * Math.sin(angle * i)
        );
      }
      ctx.closePath();
    }
    ctx.fillStyle = this.color;
    ctx.fill();
  }

  update() {
    this.x += this.velocityX;
    this.y += this.velocityY;

    if (this.x + this.radius > canvas.width || this.x - this.radius < 0) {
      this.velocityX = -this.velocityX;
      this.changeShape();
    }

    if (this.y + this.radius > canvas.height || this.y - this.radius < 0) {
      this.velocityY = -this.velocityY;
      this.changeShape();
    }

    this.draw();
  }

  hover() {
    canvas.addEventListener("mousemove", (event) => {
      const dx = this.x - event.clientX;
      const dy = this.y - event.clientY;
      const distance = Math.sqrt(dx * dx + dy * dy);

      if (distance < 100) {
        this.velocityX = dx / 20;
        this.velocityY = dy / 20;
      }
    });
  }

  changeShape() {
    this.shape = shapes[Math.floor(Math.random() * shapes.length)]; // Randomly select a new shape
    this.color = colors[Math.floor(Math.random() * colors.length)]; // Randomly select a new color
  }
}

function init() {
  for (let i = 0; i < 100; i++) {
    const radius = Math.random() * 20 + 10;
    const x = Math.random() * (canvas.width - radius * 2) + radius;
    const y = Math.random() * (canvas.height - radius * 2) + radius;
    const shape = shapes[Math.floor(Math.random() * shapes.length)]; // Randomly select a shape
    const color = colors[Math.floor(Math.random() * colors.length)]; // Randomly select a color
    const particle = new Particle(x, y, radius, shape, color);
    particle.hover();
    particles.push(particle);
  }
}

function animate() {
  requestAnimationFrame(animate);
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  particles.forEach((particle) => {
    particle.update();
  });
}

init();
animate();
