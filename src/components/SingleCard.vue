<template>
  <div class="card">
    <div>
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
  props: ["card"],
  methods: {
    getImgUrl(imgUrl) {
      const images = require(`@/assets/images/${imgUrl}.png`);
      return images;
    },
    handleClick() {
      this.$emit("handle-choice", this.card);
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
</style>
