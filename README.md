<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Valentine Quiz 💘</title>

<style>
body {
  font-family: 'Comic Sans MS', cursive;
  background: linear-gradient(135deg, #ff9a9e, #fad0c4);
  text-align: center;
  padding: 20px;
  overflow-x: hidden;
}

.question {
  background: white;
  padding: 20px;
  margin: 25px auto;
  border-radius: 18px;
  width: 90%;
  max-width: 520px;
  display: none;
}

.question.active {
  display: block;
}

button {
  padding: 12px 22px;
  margin: 10px;
  border-radius: 25px;
  border: none;
  cursor: pointer;
  font-size: 16px;
  background: #ff6f91;
  color: white;
}

button:hover {
  transform: scale(1.05);
}

#noBtn {
  position: absolute;
}

/* SPOOKY POPUP */
#spookyPopup {
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,0.85);
  display: none;
  align-items: center;
  justify-content: center;
  z-index: 999;
}

#popupBox {
  background: #1a1a1a;
  color: #fff;
  padding: 30px;
  border-radius: 20px;
  width: 80%;
  max-width: 400px;
  animation: shake 0.8s infinite alternate;
  box-shadow: 0 0 20px red;
}

@keyframes shake {
  0% { transform: rotate(-1deg); }
  100% { transform: rotate(1deg); }
}

.floating {
  animation: float 2s infinite ease-in-out;
}

@keyframes float {
  0% { transform: translateY(0); }
  50% { transform: translateY(-10px); }
  100% { transform: translateY(0); }
}

#confetti {
  position: fixed;
  inset: 0;
  pointer-events: none;
  display: none;
}
</style>
</head>

<body>

<h1>💘 Valentine Special Quiz 💘</h1>

<audio autoplay loop>
  <source src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3" type="audio/mpeg">
</audio>

<div class="question active" id="q1">
<p>1️⃣ What combo did we wear on our first date?</p>
<button onclick="correct(2)">Blue & Green</button>
<button onclick="wrong()">White & Pink</button>
<button onclick="wrong()">Grey & Yellow</button>
<button onclick="wrong()">Yellow & Green</button>
</div>

<div class="question" id="q2">
<p>2️⃣ Where is our dream honeymoon location?</p>
<button onclick="wrong()">Bhutan</button>
<button onclick="wrong()">Goa</button>
<button onclick="correct(3)">Japan</button>
<button onclick="wrong()">Ganpatipule</button>
</div>

<div class="question" id="q3">
<p>3️⃣ What do I want to do on next date?</p>
<button onclick="correct(4)">Nehru Planetarium</button>
<button onclick="correct(4)">Picnic date</button>
<button onclick="correct(4)">Beach date</button>
<button onclick="correct(4)">Bloom Badaboom</button>
</div>

<div class="question" id="q4">
<p>4️⃣ What are you wearing on our next date?</p>
<button onclick="wrong()">Grey pants & yellow polo</button>
<button onclick="wrong()">Blue shirt & grey pants</button>
<button onclick="wrong()">Jeans & pink shirt</button>
<button onclick="correct(5)">Grey tshirt & blue jeans</button>
</div>

<div class="question" id="q5">
<p>5️⃣ Will you be my Valentine sweetums? 💖</p>
<button onclick="yesValentine()">YES</button>
<button id="noBtn">NO</button>
</div>

<!-- SPOOKY POPUP -->
<div id="spookyPopup">
  <div id="popupBox">
    <h2 class="floating">👻 I knew u’d say YES bb 😌</h2>
    <p class="floating">Of course u are my Valentine…</p>
    <p class="floating">who else was it gonna be? 👻 sus</p>
    <p class="floating">💀💘💀</p>
  </div>
</div>

<canvas id="confetti"></canvas>

<script>
function wrong() {
  alert("❌ You are ded 💀");
}

function correct(next) {
  document.querySelector(".question.active").classList.remove("active");
  document.getElementById("q" + next).classList.add("active");
}

function yesValentine() {
  startConfetti();
  document.getElementById("spookyPopup").style.display = "flex";
}

const noBtn = document.getElementById("noBtn");
let chaseStart = null;

document.addEventListener("mousemove", (e) => {
  const rect = noBtn.getBoundingClientRect();
  const dist = Math.hypot(
    e.clientX - (rect.left + rect.width/2),
    e.clientY - (rect.top + rect.height/2)
  );

  if (dist < 120) {
    if (!chaseStart) chaseStart = Date.now();
    noBtn.style.left = Math.random() * (window.innerWidth - 120) + "px";
    noBtn.style.top = Math.random() * (window.innerHeight - 60) + "px";

    if (Date.now() - chaseStart > 5000) {
      alert("Your answer has been recorded and you've been rejected for Valentine’s 💔");
      chaseStart = null;
    }
  }
});

// CONFETTI
function startConfetti() {
  const canvas = document.getElementById("confetti");
  const ctx = canvas.getContext("2d");
  canvas.style.display = "block";
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;

  const pieces = Array.from({length: 150}, () => ({
    x: Math.random()*canvas.width,
    y: Math.random()*canvas.height,
    r: Math.random()*6 + 4,
    d: Math.random()*30
  }));

  setInterval(() => {
    ctx.clearRect(0,0,canvas.width,canvas.height);
    pieces.forEach(p => {
      ctx.beginPath();
      ctx.arc(p.x,p.y,p.r,0,Math.PI*2);
      ctx.fillStyle = "hsl(" + Math.random()*360 + ",100%,50%)";
      ctx.fill();
      p.y += 3;
      if (p.y > canvas.height) p.y = -10;
    });
  }, 20);
}
</script>

</body>
</html>
