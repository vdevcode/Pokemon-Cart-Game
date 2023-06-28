<template>
  <div class="screen-card">
    <h1>Interact Components here</h1>
    <CardFlip />
  </div>
</template>

<script>
import CardFlip from "@/components/CardFlip.vue";
export default {
  name: "InteractScreen",
  components: {
    CardFlip,
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
