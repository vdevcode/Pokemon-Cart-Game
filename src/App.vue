<template>
  <h1>Game Pokemon</h1>
  <MainScreen
    v-if="statusMatch === 'default'"
    @onStart="onHandleBeforeStart($event)"
  />
  <InteractScreen
    v-if="statusMatch == 'match'"
    :cardsContext="settings.cardsContext"
  />
</template>

<script>
import MainScreen from "@/components/MainScreen.vue";
import InteractScreen from "@/components/InteractScreen.vue";

import { shuffle } from "@/utils/array.js";

export default {
  name: "App",
  data() {
    return {
      settings: {
        totalOfBlocks: 0,
        cardsContext: [],
        startedAt: null,
      },
      statusMatch: "default",
    };
  },
  components: {
    MainScreen,
    InteractScreen,
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
  },
};
</script>
