<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Flashcard Viewer</title>
  <style>
    * {
      box-sizing: border-box;
    }
    body {
      font-family: sans-serif;
      background: #f4f4f4;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 2rem;
      margin: 0;
    }
    h1 {
      margin-bottom: 1rem;
    }
    .flashcard-container {
      perspective: 1000px;
      width: 300px;
      height: 200px;
      margin-bottom: 1rem;
    }
    .flashcard {
      width: 100%;
      height: 100%;
      position: relative;
      transition: transform 0.6s;
      transform-style: preserve-3d;
      cursor: pointer;
    }
    .flashcard.flipped {
      transform: rotateY(180deg);
    }
    .card-face {
      position: absolute;
      width: 100%;
      height: 100%;
      backface-visibility: hidden;
      background: white;
      border: 1px solid #ccc;
      border-radius: 8px;
      padding: 1rem;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 1.2rem;
    }
    .card-back {
      transform: rotateY(180deg);
    }
    .buttons {
      display: flex;
      gap: 1rem;
      margin-bottom: 1rem;
    }
    button {
      padding: 0.5rem 1rem;
      border: none;
      border-radius: 5px;
      font-size: 1rem;
      cursor: pointer;
      transition: background 0.3s;
    }
    .know {
      background-color: #4caf50;
      color: white;
    }
    .dont-know {
      background-color: #f44336;
      color: white;
    }
    .counter {
      font-size: 1rem;
    }
  </style>
</head>
<body>
  <h1>Flashcard Viewer</h1>
  <div class="flashcard-container" onclick="flipCard()">
    <div class="flashcard" id="flashcard">
      <div class="card-face card-front" id="card-front">Question</div>
      <div class="card-face card-back" id="card-back">Answer</div>
    </div>
  </div>

  <div class="buttons">
    <button class="know" onclick="markAnswer(true)">Know</button>
    <button class="dont-know" onclick="markAnswer(false)">Don’t Know</button>
  </div>

  <div class="counter" id="counter">Card 1 of 3</div>

  <script>
    const cards = [
      { front: "What is the capital of France?", back: "Paris" },
      { front: "2 + 2 equals?", back: "4" },
      { front: "HTML stands for?", back: "HyperText Markup Language" },
    ];

    let current = 0;
    let flipped = false;

    const flashcard = document.getElementById("flashcard");
    const front = document.getElementById("card-front");
    const back = document.getElementById("card-back");
    const counter = document.getElementById("counter");

    function loadCard() {
      const card = cards[current];
      front.textContent = card.front;
      back.textContent = card.back;
      flashcard.classList.remove("flipped");
      flipped = false;
      counter.textContent = `Card ${current + 1} of ${cards.length}`;
    }

    function flipCard() {
      flipped = !flipped;
      flashcard.classList.toggle("flipped", flipped);
    }

    function markAnswer(known) {
      // Optionally track score here
      current++;
      if (current < cards.length) {
        loadCard();
      } else {
        flashcard.innerHTML = `<div class="card-face card-front">🎉 Done!</div>`;
        document.querySelector(".buttons").style.display = "none";
        counter.textContent = `You finished all ${cards.length} cards!`;
      }
    }

    loadCard();
  </script>
</body>
</html>
