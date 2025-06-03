Birthday Surprise
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Drag Papers ❤️</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Zeyada&display=swap');

    body {
      height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;

      background-size: 1000px;
      background-image: url("https://www.psdgraphics.com/wp-content/uploads/2022/01/white-math-paper-texture.jpg");
      background-position: center center;
    }

    .paper {
      background-image: url("https://i0.wp.com/textures.world/wp-content/uploads/2018/10/2-Millimeter-Paper-Background-copy.jpg?ssl=1");
      background-size: 500px;
      background-position: center center;
      padding: 20px 100px;
      /*  min-width: 800px; */

      transform: rotateZ(-5deg);
      box-shadow: 1px 15px 20px 0px rgba(0,0,0,0.5);

      position: absolute;
    }

    .paper.heart {
      position: relative;
      width: 200px;
      height: 200px;
      padding: 0;
      border-radius: 50%;
    }

    .paper.image {
      padding: 10px;
    }
    .paper.image p {
      font-size: 30px;
    }

    img {
      max-height: 200px;
      width: 100%;
      user-select: none;
    }

    .paper.heart::after {
      content: "";
      background-image: url('https://cdn.pixabay.com/photo/2016/03/31/19/25/cartoon-1294994__340.png');
      width: 100%;
      height: 100%;
      position: absolute;
      top: 0;
      left: 0;
      background-size: 150px;
      background-position: center center;
      background-repeat: no-repeat;
      opacity: 0.6;
    }

    p {
      font-family: 'Zeyada';
      font-size: 50px;
      color: rgb(0,0,100);
      opacity: 0.75;
      user-select: none;
      /* filter: drop-shadow(2px 1.5px 1px rgba(0,0,105,0.9)); */
    }
  </style>
</head>
<body>

  <!-- Papers -->
  <div class="paper heart"></div>

  <div class="paper image">
    <p>Things To Remember :</p>
    <p>My Phone Misses Your Message</p>
    <p>We Will Meet Super Soon</p>
    <img src="ojasvi.jpg" alt="Image 1" />
  </div>

  <div class="paper image">
    <p>Congratulations For Clearing</p>
    <p>Another Level Of This Hardcore Game</p>
    <img src="Ojasvu.png" alt="Image 2" />
  </div>

  <div class="paper image">
    <p>Are You Made Of Stardust?</p>
    <p>Because Everytime I Look At You❤️</p>
    <p>I Feel Like I'm In A Dream</p>
    <img src="Ojasvi 1.jpg" alt="Image 3" />
  </div>

  <div class="paper red">
    <p class="p1"> You Are One Of My Favorite</p>
    <p class="p2">Person I Met In My Life😍</p>
  </div>

  <div class="paper">
    <p class="p1">Wishing You a day filled with smiles </p>
    <p class="p1">Happy Birthday Ojasvi Verma <span style="color: red !important;">❤️</span></p>
  </div>

  <div class="paper">
    <p class="p1">Drag the papers to move!</p>
  </div>

  <script>
    let highestZ = 1;

    class Paper {
      holdingPaper = false;
      mouseTouchX = 0;
      mouseTouchY = 0;
      mouseX = 0;
      mouseY = 0;
      prevMouseX = 0;
      prevMouseY = 0;
      velX = 0;
      velY = 0;
      rotation = Math.random() * 30 - 15;
      currentPaperX = 0;
      currentPaperY = 0;
      rotating = false;

      init(paper) {
        document.addEventListener('mousemove', (e) => {
          if(!this.rotating) {
            this.mouseX = e.clientX;
            this.mouseY = e.clientY;

            this.velX = this.mouseX - this.prevMouseX;
            this.velY = this.mouseY - this.prevMouseY;
          }

          const dirX = e.clientX - this.mouseTouchX;
          const dirY = e.clientY - this.mouseTouchY;
          const dirLength = Math.sqrt(dirX*dirX+dirY*dirY);
          const dirNormalizedX = dirX / dirLength;
          const dirNormalizedY = dirY / dirLength;

          const angle = Math.atan2(dirNormalizedY, dirNormalizedX);
          let degrees = 180 * angle / Math.PI;
          degrees = (360 + Math.round(degrees)) % 360;
          if(this.rotating) {
            this.rotation = degrees;
          }

          if(this.holdingPaper) {
            if(!this.rotating) {
              this.currentPaperX += this.velX;
              this.currentPaperY += this.velY;
            }
            this.prevMouseX = this.mouseX;
            this.prevMouseY = this.mouseY;

            paper.style.transform = `translateX(${this.currentPaperX}px) translateY(${this.currentPaperY}px) rotateZ(${this.rotation}deg)`;
          }
        });

        paper.addEventListener('mousedown', (e) => {
          if(this.holdingPaper) return;
          this.holdingPaper = true;

          paper.style.zIndex = highestZ;
          highestZ += 1;

          if(e.button === 0) {
            this.mouseTouchX = this.mouseX;
            this.mouseTouchY = this.mouseY;
            this.prevMouseX = this.mouseX;
            this.prevMouseY = this.mouseY;
          }
          if(e.button === 2) {
            this.rotating = true;
          }
        });
        window.addEventListener('mouseup', () => {
          this.holdingPaper = false;
          this.rotating = false;
        });
      }
    }

    const papers = Array.from(document.querySelectorAll('.paper'));

    papers.forEach(paper => {
      const p = new Paper();
      p.init(paper);
    });
  </script>
</body>
</html>
