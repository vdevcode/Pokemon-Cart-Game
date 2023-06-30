<template>
  <div class="screen">
    <h1>Interact Components here</h1>
    <div
      class="screen__inner"
      :style="{
        width: `${
          ((((920 - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 3) / 4 +
            16) *
          Math.sqrt(cardsContext.length)
        }px`,
      }"
    >
      <CardFlip
        v-for="(card, index) in cardsContext"
        :key="index"
        :ref="`card-${index}`"
        :imgBackFaceUrl="`images/${card}.png`"
        :card="{ index, value: card }"
        @onFlip="checkRule($event)"
        :cardsContext="cardsContext"
      />
    </div>
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
  components: {
    CardFlip,
  },
  data() {
    return {
      rules: [],
    };
  },
  methods: {
    checkRule(card) {
      console.log(card);
      if (this.rules.length === 2) {
        return false;
      }
      this.rules.push(card);
      if (
        this.rules.length === 2 &&
        this.rules[0].value === this.rules[1].value &&
        this.rules[0].index != this.rules[1].index
      ) {
        console.log("right");
        this.$refs[`card-${this.rules[0].index}`][0].onEnabelDisableCard();
        this.$refs[`card-${this.rules[1].index}`][0].onEnabelDisableCard();
        this.rules = [];
        const disabledElements = document.querySelectorAll(
          ".screen .card.disabled"
        );
        if (
          disabledElements &&
          disabledElements.length === this.cardsContext.length - 2
        ) {
          setTimeout(() => {
            this.$emit("onFinished");
          }, 920);
        }
      } else if (
        this.rules.length === 2 &&
        this.rules[0].value !== this.rules[1].value
      ) {
        console.log("wrong");
        setTimeout(() => {
          this.$refs[`card-${this.rules[0].index}`][0].onFlipBackCard();
          this.$refs[`card-${this.rules[1].index}`][0].onFlipBackCard();
          this.rules = [];
        }, 400);
      } else return false;
    },
  },
};
</script>

<style scoped>
.screen {
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  z-index: 2;
  background-color: var(--dark);
  color: var(--light);
  padding: 1rem;
}
.screen__inner {
  width: 424px;
  display: flex;
  flex-wrap: wrap;
  margin: 2rem auto;
}
</style>
