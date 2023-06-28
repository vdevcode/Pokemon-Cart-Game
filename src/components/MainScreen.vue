<template>
  <div class="screen">
    <h1>poke memories</h1>
    <h3>select mode to start game</h3>
    <div class="actions">
      <button @click="onStart(16)">
        <span>4x4</span>
        <span>easy</span>
      </button>
      <button @click="onStart(36)">
        <span>6x6</span>
        <span>normal</span>
      </button>
      <button @click="onStart(64)">
        <span>8x8</span>
        <span>hard</span>
      </button>
      <button @click="onStart(100)">
        <span>10x10</span>
        <span>super hard</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "MainScreen",
  methods: {
    onStart(totalOfBlocks) {
      this.$emit("onStart", { totalOfBlocks });
    },
  },
};
</script>
