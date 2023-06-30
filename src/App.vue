<template>
  <MainScreen
    v-if="statusMatch === 'default'"
    @onStart="onHandleBeforeStart($event)"
  />
  <InteractScreen
    @onFinished="onGetResult"
    v-if="statusMatch == 'match'"
    :cardsContext="settings.cardsContext"
  />
  <ResultScreen
    :timer="timer"
    v-if="statusMatch === 'result'"
    @onStartAgain="statusMatch = 'default'"
  />
  <CoppyRightScreen />
</template>

<script>
import MainScreen from "@/components/MainScreen.vue";
import InteractScreen from "@/components/InteractScreen.vue";
import ResultScreen from "@/components/ResultScreen.vue";
import CoppyRightScreen from "./components/CoppyRightScreen.vue";
import { shuffle } from "@/utils/array.js";

export default {
  name: "App",
  components: {
    MainScreen,
    InteractScreen,
    ResultScreen,
    CoppyRightScreen,
  },
  data() {
    return {
      settings: {
        totalOfBlocks: 0,
        cardsContext: [],
        startedAt: null,
      },
      statusMatch: "default",
      timer: 0,
    };
  },
  methods: {
    onHandleBeforeStart(config) {
      this.settings.totalOfBlocks = config.totalOfBlocks;
      const firstCards = Array.from(
        { length: this.settings.totalOfBlocks / 2 },
        (_, i) => i + 1
      );
      const secondCards = [...firstCards];
      const cards = [...firstCards, ...secondCards];
      this.settings.cardsContext = shuffle(shuffle(shuffle(shuffle(cards))));
      console.log(this.settings.cardsContext);
      this.settings.startedAt = new Date().getTime();

      //load data
      this.statusMatch = "match";
    },
    onGetResult() {
      this.timer = new Date().getTime() - this.settings.startedAt;
      this.statusMatch = "result";
    },
  },
};
</script>

<style scoped>
.coppyright {
  position: fixed;
  left: 50%;
  transform: translateX(-50%);
  bottom: 0rem;
  color: var(--light);
  z-index: 3;
  font-size: 1rem;
}
.coppyright a {
  color: yellow !important;
}
</style>
