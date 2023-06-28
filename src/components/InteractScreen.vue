<template>
  <div class="screen-card">
    <h1>Interact Components here</h1>
    <CardFlip
      v-for="(card, index) in cardsContext"
      :key="index"
      :imgBackFaceUrl="`images/${card}.png`"
      :card="card"
      @onFlip="checkRule($event)"
    />
  </div>
</template>

<script>
import CardFlip from "@/components/CardFlip.vue";
export default {
  name: "InteractScreen",
  props: {
    cardsContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  data() {
    return {
      rules: [],
    };
  },
  components: {
    CardFlip,
  },
  methods: {
    checkRule(card) {
      if (this.rules.length === 2) {
        return false;
      }
      this.rules.push(card);
      console.log(this.rules);

      if (this.rules.length === 2 && this.rules[0] === this.rules[1]) {
        return true;
        // console.log('right');
      } else if (this.rules.length === 2 && this.rules[0] !== this.rules[1]) {
        return false;
      }
    },
  },
};
</script>
<!-- 
<style scoped>
.screen-card {
  width: 100%;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
  background-color: var(--dark);
  color: var(--light);
}
</style> -->
