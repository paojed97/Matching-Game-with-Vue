<template>
  <div class="App">
    <h1>Magic Match</h1>
    <button @click="shuffleCards">New Game</button>

    <div class="card-grid">
      <SingleCard
        v-for="card in cards"
        :key="card.id"
        :card="card"
        @handle-choice="handleChoice"
        :flipped="flipped(card)"
      />
    </div>
  </div>

  <div>{{ choiceOne }}</div>
  <div>{{ choiceTwo }}</div>
</template>

<script>
import SingleCard from "./components/SingleCard.vue";

export default {
  name: "App",
  components: { SingleCard },
  data() {
    return {
      cardImages: [
        { src: "helmet-1", matched: false },
        { src: "potion-1", matched: false },
        { src: "ring-1", matched: false },
        { src: "scroll-1", matched: false },
        { src: "shield-1", matched: false },
        { src: "sword-1", matched: false },
      ],
      cards: [],
      turns: 0,
      choiceOne: null,
      choiceTwo: null,
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
    // handle a choice
    handleChoice(card) {
      this.choiceOne ? (this.choiceTwo = card) : (this.choiceOne = card);
    },
    // reset choices & increase turn
    resetTurn() {
      this.choiceOne = null;
      this.choiceTwo = null;
      this.turns += 1;
    },
  },
  mounted() {
    this.shuffleCards();
  },
  // compare two selected cards
  updated() {
    if (this.choiceOne && this.choiceTwo) {
      if (this.choiceOne.src === this.choiceTwo.src) {
        this.cards = this.cards.map((card) => {
          if (card.src === this.choiceOne.src) {
            return { ...card, matched: true };
          } else {
            return card;
          }
        });
        this.resetTurn();
      } else {
        setTimeout(() => this.resetTurn(), 1000);
      }
    }
  },
  computed: {
    flipped() {
      return (card) =>
        card === this.choiceOne || card === this.choiceTwo || card.matched;
    },
  },
};
</script>

<style>
@import "./assets/base.css";
</style>
