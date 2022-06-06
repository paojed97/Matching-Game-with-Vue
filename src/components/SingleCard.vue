<template>
  <div class="card" :class="{ matched: matched }">
    <div :class="{ flipped: flipped }">
      <img :src="getImgUrl(card.src)" alt="card front" class="front" />
      <img
        src="@/assets/images/cover.png"
        @click="handleClick"
        alt="card back"
        class="back"
      />
    </div>
  </div>
</template>

<script>
export default {
  props: ["card", "flipped", "disabled", "matched"],
  methods: {
    getImgUrl(imgUrl) {
      const images = require(`@/assets/images/${imgUrl}.png`);
      return images;
    },
    handleClick() {
      if (!this.disabled) {
        this.$emit("handle-choice", this.card);
      }
    },
  },
};
</script>

<style>
.card {
  position: relative;
}

.card img {
  width: 100%;
  display: block;
  border: 2px solid #fff;
  border-radius: 6px;
}

/* front of card - the picture */
.card .front {
  transform: rotateY(90deg);
  transition: all ease-in 0.2s;
  position: absolute;
}

.flipped .front {
  transform: rotateY(0deg);
  transition-delay: 0.2s;
}

/* back of card - cover */
.card .back {
  transition: all ease-in 0.2s;
  transition-delay: 0.2s;
}

.flipped .back {
  transform: rotateY(90deg);
  transition-delay: 0s;
}

/* animation when cards match */
.matched {
  animation: flip-out-hor-top 0.45s ease-out 1.2s both;
}

@keyframes flip-out-hor-top {
  0% {
    transform: rotateX(0deg);
    opacity: 1;
  }
  100% {
    transform: rotateX(70deg);
    opacity: 0;
  }
}
</style>
