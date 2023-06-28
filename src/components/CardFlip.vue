<template>
  <div class="card">
    <div
      class="card__inner"
      :class="{ 'is-flipped': isFlipped }"
      @click="onToggleFlipCard"
    >
      <div class="card__face card__face--front">
        <div class="card__content">front</div>
      </div>
      <div class="card__face card__face--back">
        <div class="card__content">back</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isFlipped: false,
    };
  },
  methods: {
    onToggleFlipCard() {
      this.isFlipped = !this.isFlipped;
    },
  },
};
</script>

<style scoped lang="css">
.card {
  display: inline-block;
  margin: 0 1rem 1rem 0;
  width: 90px;
  height: 120px;
}
.card__inner.is-flipped {
  transform: rotateY(-180deg);
  transition: 0.5s;
}
.card__inner {
  width: 100%;
  height: 100%;
  transition: transform 1s;
  transform-style: preserve-3d;
  cursor: pointer;
  position: relative;
}

.card__face {
  position: absolute;
  backface-visibility: hidden;
  overflow: hidden;
  border-radius: 1rem;
  padding: 1rem;
  box-shadow: 0 3px 18px 3px rgba(0, 0, 0, 0.2);
  width: 100%;
  height: 100%;
}
.card__face--back {
  background-color: var(--light);
  transform: rotateY(-180deg);
}
</style>
