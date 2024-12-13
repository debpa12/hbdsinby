

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Heart Timer Animation</title>
  <style>
    body {
      margin: 0;
      background: linear-gradient(135deg, #121112de, #070707, #000000);
      background-size: 400% 400%;
      animation: gradientAnimation 10s ease infinite;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      font-family: 'Arial', sans-serif;
      overflow: hidden;
    }

    @keyframes gradientAnimation {
      0% { background-position: 0% 50%; }
      50% { background-position: 100% 50%; }
      100% { background-position: 0% 50%; }
    }

    .intro-text {
      position: absolute;
      font-size: 2rem;
      color: white;
      text-align: center;
      opacity: 1;
      animation: fadeOut 3s ease forwards;
    }

    @keyframes fadeOut {
      0% { opacity: 1; }
      100% { opacity: 0; }
    }

    .svg-container {
      position: relative;
      width: 500px;
      height: 500px;
      opacity: 0;
      animation: fadeIn 2s ease-in forwards;
      animation-delay: 3s; /* Delay after intro text */
    }

    @keyframes fadeIn {
      from { opacity: 0; }
      to { opacity: 1; }
    }

    .heart-path {
      fill: none;
      stroke: rgb(225, 5, 5);
      stroke-width: 3;
      stroke-dasharray: 1200; /* Total path length */
      stroke-dashoffset: 1200; /* Start completely hidden */
      animation: drawHeart 3s ease-in-out forwards;
      animation-delay: 3.5s; /* Ensure the heart starts after fade-in */
    }

    @keyframes drawHeart {
      to {
        stroke-dashoffset: 0; /* Fully visible */
      }
    }

    .text {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      text-align: center;
      color: white;
      font-size: 1.5rem;
      font-weight: bold;
    }

    .timer {
      font-size: 1.2rem;
      margin-top: 10px;
    }
  </style>
</head>
<body>
  <!-- Teks Intro -->
  <div class="intro-text">For Sinby</div>

  <!-- Kontainer SVG untuk hati -->
  <div class="svg-container" id="svgContainer">
    <svg viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg">
      <!-- Jalur Hati -->
      <path
        class="heart-path"
        d="
          M50 20 
          C15 -10, -20 40, 50 90 
          C120 40, 85 -10, 50 20 Z
        " />
    </svg>
    <!-- Ucapan dan Timer -->
    <div class="text">
      <div>B'day Beautiful Girl ❤</div>
      <div class="timer" id="timer">Loading...</div>
    </div>
  </div>

  <script>
    // Tampilkan hati setelah intro selesai
    setTimeout(() => {
      const svgContainer = document.getElementById("svgContainer");
      svgContainer.style.opacity = 1; // Munculkan hati dan timer
    }, 3000); // Setelah 3 detik (intro selesai)

    // Tanggal awal: 13 Desember 2007
    const startDate = new Date("2007-12-13T00:00:00");

    function updateTimer() {
      const currentTime = new Date();
      const elapsed = currentTime - startDate; // Selisih waktu dalam milidetik

      const days = Math.floor(elapsed / (1000 * 60 * 60 * 24));
      const hours = Math.floor((elapsed % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
      const minutes = Math.floor((elapsed % (1000 * 60 * 60)) / (1000 * 60));
      const seconds = Math.floor((elapsed % (1000 * 60)) / 1000);

      document.getElementById('timer').textContent =
        `${days} days ${hours} hours ${minutes} minutes ${seconds} seconds`;

      requestAnimationFrame(updateTimer);
    }

    // Timer dimulai setelah animasi hati selesai
    setTimeout(updateTimer, 3500); // Mulai timer setelah animasi hati muncul
  </script>
</body>
</html>
