<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Aesthetic Trends Research</title>

  <!-- Load p5.js -->
  <script src="https://cdn.jsdelivr.net/npm/p5@1.9.0/lib/p5.min.js"></script>

  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: 'Futura', sans-serif;
      background-color: #c6b0f3;
      color: #000000;
      overflow: hidden;
    }

    .container {
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 60px 80px;
      position: relative;
      z-index: 10;
    }

    .left-content {
      max-width: 45%;
      z-index: 10;
    }

    .title {
      font-size: 120px;
      line-height: 0.95;
      font-weight: 300;
      font-style: italic;
      color: #ffffff;
      margin-bottom: 60px;
      letter-spacing: -2px;
    }

    .info-list {
      list-style: none;
      margin-bottom: 50px;
    }

    .info-list li {
      font-size: 26px;
      margin-bottom: 8px;
      color: #4a4a4a;
      display: flex;
      align-items: baseline;
    }

    .info-list .number {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      width: 28px;
      height: 28px;
      border: 1px solid #4a4a4a;
      border-radius: 50%;
      font-size: 14px;
      margin-right: 12px;
      flex-shrink: 0;
    }

    .description {
      font-size: 15px;
      line-height: 1.6;
      color: #6a6a6a;
      max-width: 500px;
      margin-bottom: 30px;
    }

    canvas {
      position: fixed;
      top: 0;
      left: 0;
      z-index: 1;
    }
  </style>
</head>

<body>
  <div class="container">
    <div class="left-content">
      <h1 class="title">Aesthetic<br>Trends</h1>

      <ul class="info-list">
        <li><span class="number">1</span> AR & Interactive Design</li>
        <li><span class="number">2</span> Colorful Visuals</li>
        <li><span class="number">3</span> Sound & Music Impact</li>
        <li><span class="number">4</span> Emotional Engagement</li>
      </ul>

      <p class="description">
        THIS STUDY EXPLORES HOW AESTHETIC TRENDS IN ADVERTISING AND DESIGN INCREASE CONSUMER APPEAL. ANALYZING DATA FROM 176 PARTICIPANTS ACROSS VARIOUS DEMOGRAPHICS.
      </p>

      <p class="description">
        THE FINDINGS REVEALED THAT 37.4% OF EXPERTS CONSIDER AR & INTERACTIVE DESIGN MOST EFFECTIVE, WHILE 40.8% IDENTIFIED SOUND & MUSIC AS THE MOST IMPACTFUL ELEMENT. 28.4% OF CONSUMERS EXPERIENCE BRAND IDENTITY THROUGH AESTHETIC DESIGN.
      </p>
    </div>
  </div>

  <!-- Interactive p5.js background -->
  <script>
    let balls = [];

    function setup() {
      createCanvas(windowWidth, windowHeight);
      noStroke();
      for (let i = 0; i < 30; i++) {
        balls.push(new Ball());
      }
    }

    function draw() {
      background(198, 176, 243, 40); // soft lavender translucent background
      for (let b of balls) {
        b.move();
        b.followMouse();
        b.display();
      }
    }

    class Ball {
      constructor() {
        this.x = random(width);
        this.y = random(height);
        this.d = random(10, 40);
        this.xspeed = random(-1, 1);
        this.yspeed = random(-1, 1);
        this.color = color(
          random(230, 255),
          random(190, 220),
          random(240, 255),
          180
        );
      }

      move() {
        this.x += this.xspeed;
        this.y += this.yspeed;

        // bounce off edges
        if (this.x < 0 || this.x > width) this.xspeed *= -1;
        if (this.y < 0 || this.y > height) this.yspeed *= -1;
      }

      followMouse() {
        // subtle attraction toward mouse
        let dx = mouseX - this.x;
        let dy = mouseY - this.y;
        let distance = sqrt(dx * dx + dy * dy);
        let force = constrain(100 / (distance + 50), 0, 0.05);
        this.xspeed += dx * force;
        this.yspeed += dy * force;

        // limit speed
        this.xspeed = constrain(this.xspeed, -3, 3);
        this.yspeed = constrain(this.yspeed, -3, 3);
      }

      display() {
        fill(this.color);
        ellipse(this.x, this.y, this.d);
      }
    }

    function windowResized() {
      resizeCanvas(windowWidth, windowHeight);
    }
  </script>
</body>
</html>
