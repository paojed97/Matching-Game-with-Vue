<template>
  <div class="App">
    <h1>Magic Match</h1>
    <button @click="shuffleCards">New Game</button>

    <div class="card-grid">
      <SingleCard v-for="card in cards" :key="card.id" :card="card" />
    </div>
  </div>
</template>

<script>
import SingleCard from "./components/SingleCard.vue";

export default {
  name: "App",
  components: { SingleCard },
  data() {
    return {
      cardImages: [
        { src: "helmet-1" },
        { src: "potion-1" },
        { src: "ring-1" },
        { src: "scroll-1" },
        { src: "shield-1" },
        { src: "sword-1" },
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
  mounted() {
    this.shuffleCards();
  },
};
</script>

<style>
@import "./assets/base.css";
</style>
