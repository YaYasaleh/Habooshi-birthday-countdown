# Heba-birthday-countdown
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>Happy Birthday هبه ❤️</title>

  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      min-height: 100vh;
      overflow: hidden;
      font-family: Arial, sans-serif;
      color: white;

      display: flex;
      align-items: center;
      justify-content: center;
      text-align: center;

      background:
        radial-gradient(circle at 50% 20%, #3b1954 0%, #160b24 45%, #050308 100%);
    }

    /* النجوم */

    .stars {
      position: fixed;
      inset: 0;
      pointer-events: none;
    }

    .star {
      position: absolute;
      width: 2px;
      height: 2px;
      background: white;
      border-radius: 50%;
      opacity: .7;
      animation: twinkle 3s infinite ease-in-out;
    }

    @keyframes twinkle {
      0%, 100% {
        opacity: .2;
      }

      50% {
        opacity: 1;
      }
    }

    /* القلوب */

    .hearts {
      position: fixed;
      inset: 0;
      pointer-events: none;
      overflow: hidden;
    }

    .heart {
      position: absolute;
      bottom: -40px;
      animation: floatHeart linear forwards;
    }

    @keyframes floatHeart {
      0% {
        transform: translateY(0) scale(.7);
        opacity: 0;
      }

      15% {
        opacity: .8;
      }

      100% {
        transform: translateY(-110vh) scale(1.2);
        opacity: 0;
      }
    }

    /* المحتوى */

    .container {
      width: 92%;
      max-width: 850px;
      padding: 45px 25px;

      background: rgba(255,255,255,.055);
      border: 1px solid rgba(220,180,255,.18);
      border-radius: 35px;

      backdrop-filter: blur(15px);

      box-shadow:
        0 25px 90px rgba(0,0,0,.45);

      animation: appear 1.2s ease;
    }

    @keyframes appear {
      from {
        opacity: 0;
        transform: translateY(25px);
      }

      to {
        opacity: 1;
        transform: translateY(0);
      }
    }

    .small-title {
      color: #d9a5ff;
      font-size: 17px;
      letter-spacing: 5px;
      margin-bottom: 20px;
    }

    h1 {
      font-size: clamp(45px, 10vw, 85px);
      margin-bottom: 15px;

      background:
        linear-gradient(
          90deg,
          #ffffff,
          #e5c4ff,
          #ffabd9
        );

      -webkit-background-clip: text;
      background-clip: text;
      color: transparent;
    }

    .subtitle {
      font-size: clamp(20px, 4vw, 28px);
      color: #f4e7fa;
      margin-bottom: 45px;
    }

    /* العداد */

    .countdown {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 15px;
    }

    .box {
      padding: 25px 10px;

      background: rgba(255,255,255,.055);

      border: 1px solid rgba(220,180,255,.15);

      border-radius: 22px;
    }

    .number {
      display: block;

      font-size: clamp(35px, 7vw, 60px);
      font-weight: bold;

      color: #e4b7ff;
    }

    .label {
      display: block;

      margin-top: 8px;

      color: #bcaec6;
      font-size: 15px;
    }

    .bottom {
      margin-top: 40px;

      color: #c9b4d3;
      font-size: 17px;
      line-height: 2;
    }

    .cake {
      font-size: 45px;
      margin-top: 15px;
    }

    /* الجوال */

    @media (max-width: 600px) {

      body {
        overflow: auto;
      }

      .container {
        padding: 35px 18px;
      }

      .countdown {
        grid-template-columns: repeat(2, 1fr);
      }

      .box {
        padding: 20px 8px;
      }

    }

  </style>
</head>

<body>

  <div class="stars"></div>

  <div class="hearts"></div>


  <main class="container">

    <div class="small-title">
      AUGUST 22
    </div>

    <h1>
      Happy Birthday هبه
    </h1>

    <div class="subtitle">
      باقي على يومك الكبير ❤️
    </div>


    <div class="countdown">

      <div class="box">
        <span class="number" id="days">00</span>
        <span class="label">يوم</span>
      </div>

      <div class="box">
      <span class="number" id="hours">00</span>
        <span class="label">ساعة</span>
      </div>

      <div class="box">
        <span class="number" id="minutes">00</span>
        <span class="label">دقيقة</span>
      </div>

      <div class="box">
        <span class="number" id="seconds">00</span>
        <span class="label">ثانية</span>
      </div>

    </div>


    <div class="bottom">
      ما بقي إلا القليل... 🎂
    </div>

    <div class="cake">
      🎂 ❤️
    </div>

  </main>


  <script>

    /* النجوم */

    const stars =
      document.querySelector(".stars");

    for (let i = 0; i < 120; i++) {

      const star =
        document.createElement("div");

      star.className = "star";

      star.style.left =
        Math.random() * 100 + "%";

      star.style.top =
        Math.random() * 100 + "%";

      star.style.animationDelay =
        Math.random() * 3 + "s";

      stars.appendChild(star);
    }


    /* تاريخ عيد الميلاد */

    const birthday =
      new Date("2026-08-22T00:00:00+03:00").getTime();


    function updateCountdown() {

      const now =
        new Date().getTime();

      const distance =
        birthday - now;


      if (distance <= 0) {

        document.getElementById("days").textContent = "00";
        document.getElementById("hours").textContent = "00";
        document.getElementById("minutes").textContent = "00";
        document.getElementById("seconds").textContent = "00";

        document.querySelector(".subtitle").textContent =
          "اليوم هو يومك الكبير ❤️";

        document.querySelector(".bottom").textContent =
          "Happy Birthday هبه 🎂❤️";

        return;
      }


      const days =
        Math.floor(
          distance / (1000 * 60 * 60 * 24)
        );


      const hours =
        Math.floor(
          (distance / (1000 * 60 * 60)) % 24
        );


      const minutes =
        Math.floor(
          (distance / (1000 * 60)) % 60
        );


      const seconds =
        Math.floor(
          (distance / 1000) % 60
        );


      document.getElementById("days").textContent =
        String(days).padStart(2, "0");

      document.getElementById("hours").textContent =
        String(hours).padStart(2, "0");

      document.getElementById("minutes").textContent =
        String(minutes).padStart(2, "0");

      document.getElementById("seconds").textContent =
        String(seconds).padStart(2, "0");

    }


    updateCountdown();

    setInterval(
      updateCountdown,
      1000
    );


    /* القلوب */

    function createHeart() {

      const heart =
        document.createElement("div");

      heart.className = "heart";

      heart.textContent =
        Math.random() > .5
        ? "❤️"
        : "💜";


      heart.style.left =
        Math.random() * 100 + "vw";


      heart.style.fontSize =
        (14 + Math.random() * 18) + "px";


      heart.style.animationDuration =
        (5 + Math.random() * 5) + "s";


      document
        .querySelector(".hearts")
        .appendChild(heart);


      setTimeout(
        () => heart.remove(),
        10000
      );

    }


    setInterval(
      createHeart,
      1200
    );

  </script>

</body>
</html>
