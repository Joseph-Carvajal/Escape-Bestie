<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>🔐 IBM Escape Room</title>
  <style>
    body {
      font-family: 'Poppins', sans-serif;
      background: linear-gradient(135deg, #002D9C, #0043CE);
      color: #fff;
      text-align: center;
      padding: 40px;
    }
    h1 {
      font-size: 2.2em;
      margin-bottom: 10px;
      text-shadow: 0px 0px 12px #00aaff;
    }
    #logo {
      font-size: 40px;
      font-weight: bold;
      margin-bottom: 10px;
      color: #fff;
      text-shadow: 0px 0px 20px #33bbff;
    }
    .question {
      display: none;
      margin: 20px auto;
      max-width: 650px;
      background: rgba(255,255,255,0.08);
      padding: 20px;
      border-radius: 20px;
      box-shadow: 0 0 25px rgba(0,0,0,0.5);
    }
    input {
      padding: 10px;
      margin: 10px;
      border-radius: 8px;
      border: none;
      width: 80%;
      font-size: 16px;
    }
    button {
      padding: 12px 22px;
      background: linear-gradient(90deg,#FF6EC7,#FF8AE2);
      color: white;
      border: none;
      border-radius: 25px;
      cursor: pointer;
      font-size: 16px;
      font-weight: bold;
      transition: transform 0.2s, box-shadow 0.2s;
    }
    button:hover {
      transform: scale(1.05);
      box-shadow: 0 0 15px #ff99dd;
    }
    #progressBar {
      width: 100%;
      background-color: #555;
      border-radius: 10px;
      margin: 15px auto;
      height: 20px;
    }
    #progress {
      width: 0%;
      height: 100%;
      background: linear-gradient(90deg,#33bbff,#00ffcc);
      border-radius: 10px;
    }
    #timer {
      font-size: 18px;
      margin-bottom: 20px;
    }
    canvas {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
      z-index: 999;
    }
    #end h1 {
      font-size: 2.5em;
      text-shadow: 0px 0px 18px #00ffcc;
    }
    #celebrationGif {
      width: 200px;
      margin: 20px auto;
      display: block;
    }
  </style>
</head>
<body>
  <div id="logo"> THINK </div>
  <h1>🔐 BIG BLUE: Escape Room </h1>
  <div id="timer">⏳ Time left: 300s</div>
  <div id="progressBar"><div id="progress"></div></div>

  <div id="q1" class="question">
    <p>Q1 – The Name Tag<br>What do the letters IBM stand for?</p>
    <input type="text" id="a1">
    <button onclick="checkAnswer(1, 'international business machines')">Submit</button>
  </div>

  <div id="q2" class="question">
    <p>Q2 – The Big Color Lock<br>IBM is most often called “Big ___.”</p>
    <input type="text" id="a2">
    <button onclick="checkAnswer(2, 'blue')">Submit</button>
  </div>

  <div id="q3" class="question">
    <p>Q3 – The Calendar Code<br>The wall says: IBM was born more than a century ago. In what year was it founded?</p>
    <input type="text" id="a3">
    <button onclick="checkAnswer(3, '1911')">Submit</button>
  </div>

  <div id="q4" class="question">
    <p>Q4 – The Money Code<br>IBM helped banks and businesses process data faster with early machines. What’s the three-letter word for money?</p>
    <input type="text" id="a4">
    <button onclick="checkAnswer(4, 'atm')">Submit</button>
  </div>

  <div id="q5" class="question">
    <p>Q5 – The AI Room<br>IBM’s AI is named after which famous detective’s sidekick?</p>
    <input type="text" id="a5">
    <button onclick="checkAnswer(5, 'watson')">Submit</button>
  </div>

  <div id="q6" class="question">
    <p>Q6 – The Cloud Hint<br>What’s the word for storing files online instead of on your computer?</p>
    <input type="text" id="a6">
    <button onclick="checkAnswer(6, 'cloud')">Submit</button>
  </div>

  <div id="q7" class="question">
    <p>Q7 – The Final Key<br>This one-word slogan from IBM says it all. It’s short, smart, and starts with a ‘T’. What is it?</p>
    <input type="text" id="a7">
    <button onclick="checkAnswer(7, 'think')">Submit</button>
  </div>

  <div id="q8" class="question">
    <p>Q8 – The Learning Key<br>What is the name of IBM's Learning Management System?</p>
    <input type="text" id="a8">
    <button onclick="checkAnswer(8, 'yourlearning')">Submit</button>
  </div>

  <div id="end" class="question">
    <p>🎉 Congrats, you Escaped!<br>Enter your name below:</p>
    <input type="text" id="playerName">
    <button onclick="finishGame()">Submit</button>
  </div>

  <canvas id="confetti"></canvas>

  <script>
    let current = 1;
    let totalQuestions = 8;
    let timeLeft = 180;
    let timer = setInterval(function(){
      if(timeLeft <= 0){
        clearInterval(timer);
        document.body.innerHTML = "<h1>⏰ Time's up! Game Over.</h1>";
      } else {
        document.getElementById("timer").innerHTML = "⏳ Time left: " + timeLeft + "s";
      }
      timeLeft -= 1;
    }, 1000);

    function showQuestion(n) {
      document.querySelectorAll('.question').forEach(q => q.style.display = 'none');
      document.getElementById('q' + n).style.display = 'block';
      updateProgress(n);
    }

    function checkAnswer(num, correct) {
      let ans = document.getElementById('a' + num).value.toLowerCase().trim();
      if(ans === correct){
        if(num < totalQuestions){
          showQuestion(num + 1);
        } else {
          document.querySelectorAll('.question').forEach(q => q.style.display = 'none');
          document.getElementById('end').style.display = 'block';
        }
      } else {
        alert("❌ Try again bestie!");
      }
    }

    function updateProgress(n) {
      let percent = ((n-1)/totalQuestions) * 100;
      document.getElementById("progress").style.width = percent + "%";
    }

    function finishGame() {
      let name = document.getElementById('playerName').value || "Superstar";
      document.body.innerHTML = `
        <h1>🎉 YOU DID IT, ${name}! 🎉</h1>
        <img id="celebrationGif" src="https://media.giphy.com/media/3ohs4BSacFKI7A717y/giphy.gif" alt="celebration">
        <p>📸 Screenshot this and flex it in Teams chat 💬</p>
        <p>💡 You’ve unlocked growth mindset XP — keep shining, HR champ!</p>
        <button onclick="location.reload()">Play Again 🔄</button>
      `;
      startConfetti();
    }

    // Confetti Animation
    function startConfetti() {
      const canvas = document.getElementById("confetti");
      const ctx = canvas.getContext("2d");
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;

      const pieces = new Array(200).fill().map(() => ({
        x: Math.random() * canvas.width,
        y: Math.random() * canvas.height - canvas.height,
        w: 8,
        h: 8,
        color: `hsl(${Math.random() * 360}, 100%, 50%)`,
        speed: 2 + Math.random() * 4
      }));

      function draw() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        pieces.forEach(p => {
          ctx.fillStyle = p.color;
          ctx.fillRect(p.x, p.y, p.w, p.h);
          p.y += p.speed;
          if (p.y > canvas.height) p.y = -10;
        });
        requestAnimationFrame(draw);
      }
      draw();
    }

    showQuestion(1);
  </script>
</body>
</html>
