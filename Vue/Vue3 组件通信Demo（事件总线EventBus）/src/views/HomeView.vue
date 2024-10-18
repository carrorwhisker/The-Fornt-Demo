<template>
  <div class="home">
    <div class="component-row">
      <war-first></war-first>
      <war-second></war-second>
    </div>
    <div class="component-row">
      <war-third></war-third>
      <war-fourth></war-fourth>
    </div>
  </div>
</template>

<script>
import WarFirst from "@/components/WarFirst.vue";
import WarSecond from "@/components/WarSecond.vue";
import WarThird from "@/components/WarThird.vue";
import WarFourth from "@/components/WarFourth.vue";

export default {
  name: 'HomeView',
  components: {
    WarFirst,
    WarSecond,
    WarThird,
    WarFourth
  }
}
</script>

<style scoped>
.home {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.component-row {
  display: flex;
  justify-content: space-between;
  width: 100%;
}

.component-row > * {
  flex: 1;
  margin: 0 8px; /* 可以根据需要调整间距 */
}
</style>