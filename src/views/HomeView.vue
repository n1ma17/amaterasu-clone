
<template>
  <div class="home">
    <div class="home__first-step">
      <FirstStep />
    </div>
  </div>
</template>

<script setup>

import FirstStep from '@/components/FirstStep/ContentComponent.vue';

</script>
<style lang="scss" scoped>
.home {
  width: 100vw;
  height: 100vh;
  background-color: #183969;
}
</style>
