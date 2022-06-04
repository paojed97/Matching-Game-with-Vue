<template>
  <div class="App">
    <h1>Magic Match</h1>
    <button @click="shuffleCards">New Game</button>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      cardImages: [
        { src: "/assets/images/helmet-1.png" },
        { src: "/assets/images/potion-1.png" },
        { src: "/assets/images/ring-1.png" },
        { src: "/assets/images/scroll-1.png" },
        { src: "/assets/images/shield-1.png" },
        { src: "/assets/images/sword-1.png" },
      ],
      cards: [],
      turns: 0,
    };
  },
  methods: {
    // shuffle cards
    shuffleCards() {
      const shuffleCards = [...this.cardImages, ...this.cardImages]
        .sort(() => Math.random() - 0.5)
        .map((card) => ({ ...card, id: Math.random() }));

      this.cards = shuffleCards;
      this.turns = 0;
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Raleway:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap");

/* base styles */
body {
  font-family: Raleway, sans-serif;
  margin: 0;
  font-size: 1.5em;
  text-align: center;
  background: #1b1523;
  color: #fff;
}

.App {
  max-width: 860px;
  margin: 40px auto;
}

button {
  background: none;
  border: 2px solid #fff;
  padding: 6px 12px;
  border-radius: 4px;
  color: #fff;
  font-weight: bold;
  cursor: pointer;
  font-size: 1em;
}

button:hover {
  background: #c23866;
  color: #fff;
}
</style>
