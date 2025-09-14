<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Escape Bestie</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #111;
      color: #f0f0f0;
      text-align: center;
      padding: 40px;
    }
    .question {
      display: none;
      margin: 20px auto;
      max-width: 500px;
    }
    .question.active {
      display: block;
    }
    input, button {
      padding: 10px;
      margin-top: 10px;
      border-radius: 8px;
      border: none;
    }
    button {
      cursor: pointer;
      background: #4cafef;
      color: #fff;
      font-weight: bold;
    }
    #endScreen {
      display: none;
    }
    img {
      max-width: 250px;
      margin: 20px 0;
    }
  </style>
</head>
<body>
  <!-- 🎮 Game Area -->
  <div id="gameArea">
    <h1>✨ Escape Bestie ✨</h1>
    <p>Type your name to begin:</p>
    <input type="text" id="playerName" placeholder="Enter your name">
    <button onclick="startGame()">Start Game 🚀</button>

    <!-- Question 1 -->
    <div class="question" id="q1">
      <h2>What is the name of IBM's Learning Management System?</h2>
      <input type="text" id="answer1" placeholder="Your answer">
      <button onclick="checkAnswer(1)">Submit</button>
    </div>
  </div>

  <!-- 🦄 End Screen -->
  <div id="endScreen">
    <h1>🎉 YOU DID IT, <span id="winnerName"></span>! 🎉</h1>
    <img src="https://media.tenor.com/lP3A3tSxV1wAAAAC/unicorn-laptop.gif" alt="Unicorn celebration">
    <p>📸 Screenshot this and flex it in Teams chat 💬</p>
    <p>✨ You’ve unlocked growth mindset XP — keep shining, HR champ! ✨</p>
    <button onclick="location.reload()">Play Again 🔄</button>
  </div>

  <script>
    function startGame() {
      document.getElementById("q1").classList.add("active");
    }

    function checkAnswer(qNum) {
      let input = document.getElementById("answer" + qNum).value.trim().toLowerCase();
      if (qNum === 1 && input === "yourlearning") {
        finishGame();
      } else {
        alert("Not quite! Try again bestie 💡");
      }
    }

    function finishGame() {
      let name = document.getElementById("playerName").value || "Superstar";
      document.getElementById("gameArea").style.display = "none";
      document.getElementById("endScreen").style.display = "block";
      document.getElementById("winnerName").textContent = name;
    }
  </script>
</body>
</html>
