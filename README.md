<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>موزّع أوراق خاص – 8 لاعبين</title>

<style>
body {
  font-family: Arial, sans-serif;
  direction: rtl;
  text-align: center;
  padding: 20px;

  background-color: #000;
  background-image:
    linear-gradient(rgba(0,0,0,0.7), rgba(0,0,0,0.85)),
    url("https://i.ibb.co/5n3Y2yV/mafia-bg.jpg");
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;

  color: #fff;
}

input, button {
  font-size: 18px;
  padding: 10px;
  margin: 6px;
  width: 85%;
  border-radius: 8px;
  border: none;
}

input {
  background: rgba(255,255,255,0.9);
}

button {
  background: #8b0000;
  color: #fff;
}

button:disabled {
  background: #555;
  cursor: not-allowed;
}

.card {
  font-size: 42px;
  margin-top: 20px;
  min-height: 60px;
  text-shadow: 2px 2px 6px black;
}

small {
  color: #ddd;
  display: block;
  margin-top: 10px;
}
</style>
</head>

<body>

<h2>🎴 موزّع ورقة سرية (8 لاعبين)</h2>

<input id="name" placeholder="اكتب اسم اللاعب">
<button id="dealBtn">احصل على ورقتي</button>
<button id="hideBtn" disabled>إخفاء الورقة 👁️</button>

<div id="result" class="card"></div>
<small id="counter"></small>

<br><br>
<button onclick="resetGame()">🔄 جولة جديدة</button>

<script>
let deck = [];
let dealt = 0;
let currentCard = "";

function createDeck() {
  deck = [
    "Joker",
    "K♠",
    "J♥",
    "2♦", "3♣", "4♠", "5♥", "6♦"
  ];

  deck.sort(function () { return Math.random() - 0.5; });

  dealt = 0;
  currentCard = "";

  document.getElementById("result").textContent = "";
  document.getElementById("counter").textContent = "";
  document.getElementById("name").value = "";

  document.getElementById("dealBtn").disabled = false;
  document.getElementById("hideBtn").disabled = true;
}

createDeck();

document.getElementById("dealBtn").onclick = function () {
  let name = document.getElementById("name").value.trim();

  if (name === "") {
    alert("اكتب اسمك أولًا");
    return;
  }

  if (dealt >= 8) {
    alert("انتهت الجولة ❌");
    return;
  }

  currentCard = deck.pop();
  dealt++;

  document.getElementById("result").textContent = name + " → " + currentCard;
  document.getElementById("counter").textContent = "تم التوزيع: " + dealt + " من 8";

  document.getElementById("name").value = "";
  document.getElementById("dealBtn").disabled = true;
  document.getElementById("hideBtn").disabled = false;
};

document.getElementById("hideBtn").onclick = function () {
  if (currentCard === "") return;

  document.getElementById("result").textContent = "";
  currentCard = "";

  document.getElementById("dealBtn").disabled = false;
  document.getElementById("hideBtn").disabled = true;
};

function resetGame() {
  createDeck();
}
</script>

</body>
</html>
