<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>آسف</title>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html, body {
  width: 100%;
  height: 100%;
  overflow: hidden;
  background: #000;
}

canvas {
  display: block;
  width: 100%;
  height: 100%;
}
</style>
</head>

<body>

<canvas id="canvas"></canvas>

<script>
const canvas = document.getElementById("canvas");
const ctx = canvas.getContext("2d");

let particles = [];
let width;
let height;

function resize() {
  width = canvas.width = window.innerWidth * devicePixelRatio;
  height = canvas.height = window.innerHeight * devicePixelRatio;

  canvas.style.width = window.innerWidth + "px";
  canvas.style.height = window.innerHeight + "px";

  ctx.setTransform(devicePixelRatio, 0, 0, devicePixelRatio, 0, 0);

  createParticles();
}

function createParticles() {

  particles = [];

  const w = window.innerWidth;
  const h = window.innerHeight;

  /*
    نستخدم Canvas ثاني مخفي لكتابة كلمة "آسف"
    ثم نأخذ نقاط الحروف ونضع "أحبك" عليها.
  */

  const textCanvas = document.createElement("canvas");
  const textCtx = textCanvas.getContext("2d");

  textCanvas.width = w;
  textCanvas.height = h;

  const fontSize = Math.min(w * 0.48, h * 0.55);

  textCtx.font =
    900 ${fontSize}px Arial, Tahoma, sans-serif;

  textCtx.textAlign = "center";
  textCtx.textBaseline = "middle";
  textCtx.fillStyle = "white";

  textCtx.fillText(
    "آسف",
    w / 2,
    h / 2
  );

  const image = textCtx.getImageData(
    0,
    0,
    w,
    h
  );

  /*
    كل عدة بكسلات = كلمة "أحبك"
  */

  const gap = window.innerWidth < 600 ? 7 : 9;

  for (let y = 0; y < h; y += gap) {

    for (let x = 0; x < w; x += gap) {

      const index =
        (y * w + x) * 4;

      const alpha = image.data[index + 3];

      if (alpha > 100) {

        particles.push({
          x: x,
          y: y,

          offsetX: (Math.random() - 0.5) * 3,
          offsetY: (Math.random() - 0.5) * 3,

          rotation:
            (Math.random() - 0.5) * 0.15,

          opacity:
            0.45 + Math.random() * 0.55,

          size:
            window.innerWidth < 600
              ? 8 + Math.random() * 3
              : 10 + Math.random() * 4,

          phase:
            Math.random() * Math.PI * 2
        });
      }
    }
  }

  /*
    نضيف كلمات خفيفة حول الشاشة
    حتى يكون الشكل أجمل.
  */

  const extra = window.innerWidth < 600 ? 250 : 500;

  for (let i = 0; i < extra; i++) {

    particles.push({
      x: Math.random() * w,
      y: Math.random() * h,

      offsetX: 0,
      offsetY: 0,

      rotation:
        (Math.random() - 0.5) * 0.2,

      opacity:
        0.08 + Math.random() * 0.25,

      size:
        8 + Math.random() * 3,

      phase:
        Math.random() * Math.PI * 2,

      background: true
    });
  }
}

function draw(time) {

  const w = window.innerWidth;
  const h = window.innerHeight;

  ctx.clearRect(0, 0, w, h);

  ctx.fillStyle = "#000";
  ctx.fillRect(0, 0, w, h);

  for (const p of particles) {

    const movement =
      Math.sin(
        time * 0.0015 + p.phase
      ) * 1.5;

    ctx.save();

    ctx.translate(
      p.x + p.offsetX,
      p.y + p.offsetY + movement
    );

    ctx.rotate(p.rotation);

    ctx.globalAlpha = p.opacity;

    ctx.fillStyle = "#a855f7";

    ctx.font =
      600 ${p.size}px Arial, Tahoma, sans-serif;

    ctx.textAlign = "center";
    ctx.textBaseline = "middle";

    ctx.fillText(
      "أحبك",
      0,
      0
    );

    ctx.restore();
  }

  requestAnimationFrame(draw);
}

window.addEventListener(
  "resize",
  resize
);

resize();

requestAnimationFrame(draw);
</script>

</body>
</html>
