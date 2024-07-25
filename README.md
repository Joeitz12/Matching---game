# Matching---game
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Matching Game</title>
<style>
  .grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 10px;
  }
  .card {
    width: 100px;
    height: 100px;
    background-color: #333;
    color: #fff;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 2em;
    cursor: pointer;
  }
  .matched {
    background-color: #2ecc71;
  }
</style>
</head>
<body>

<div class="grid" id="gameBoard"></div>

<script>
const cards = [
  'A', 'A', 'B', 'B', 'C', 'C', 'D', 'D',
  'E', 'E', 'F', 'F', 'G', 'G', 'H', 'H'
];
let selectedCards = [];
let matchedCards = [];

function shuffle(array) {
  array.sort(() => Math.random() - 0.5);
}

function createBoard() {
  shuffle(cards);
  const gameBoard = document.getElementById('gameBoard');
  cards.forEach((card, index) => {
    const cardElement = document.createElement('div');
    cardElement.classList.add('card');
    cardElement.setAttribute('data-cardValue', card);
    cardElement.addEventListener('click', flipCard);
    gameBoard.appendChild(cardElement);
  });
}

function flipCard() {
  const cardValue = this.getAttribute('data-cardValue');
  this.innerHTML = cardValue;
  
  if (!selectedCards.includes(this)) {
    selectedCards.push(this);
    
    if (selectedCards.length === 2) {
      setTimeout(checkForMatch, 500);
    }
  }
}

function checkForMatch() {
  const [cardOne, cardTwo] = selectedCards;

  if (cardOne.innerHTML === cardTwo.innerHTML) {
    matchedCards.push(cardOne, cardTwo);
    cardOne.classList.add('matched');
    cardTwo.classList.add('matched');
    
    if (matchedCards.length === cards.length) {
      alert('You found all matches!');
    }
  } else {
    cardOne.innerHTML = '';
    cardTwo.innerHTML = '';
  }

  selectedCards = [];
}

createBoard();
</script>

</body>
</html>
