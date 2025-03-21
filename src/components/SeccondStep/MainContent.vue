<template>
  <div ref="container" class="container">
    <LogoSection />
    <DescriptionSection />
    <MindMapped />
    <QuestionsSection />
    <ChaosOrder />
    <div ref="backgroundRef" class="background"></div>
  </div>
</template>

<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
import LogoSection from './LogoSection.vue'
import DescriptionSection from './DescriptionSection.vue'
import MindMapped from './MindMapped.vue'
import QuestionsSection from './QuestionsSection.vue'
import * as THREE from 'three'
import ChaosOrder from './ChaosOrder.vue'

const backgroundRef = ref(null)
let vantaEffect = null
gsap.registerPlugin(ScrollTrigger)

onMounted(async () => {
  const VANTA = (await import('vanta/src/vanta.fog')).default

  vantaEffect = VANTA({
    el: backgroundRef.value,
    mouseControls: true,
    touchControls: true,
    gyroControls: false,
    minHeight: 200.0,
    minWidth: 200.0,
    highlightColor: 0xd0f4f9,
    midtoneColor: 0xd0f4f9,
    lowlightColor: 0xb4fcfb,
    baseColor: 0xffffff,
    blurFactor: 0.9,
    speed: 1.9,
    zoom: 0.3,
    THREE: THREE,
  })
  window.addEventListener('resize', () => {
    if (vantaEffect) {
      vantaEffect.resize()
    }
  })
})
onBeforeUnmount(() => {
  if (vantaEffect) vantaEffect.destroy()
})
</script>

<style lang="scss" scoped>
body {
  font-family: termina, sans-serif;
  transition: 0.3s ease-out;
}
.background {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw; /* عرض کل صفحه */
  height: 100vh; /* ارتفاع کل صفحه */
  z-index: -10;
  overflow: hidden;
}
.container {
  width: 100%;
  height: 100vh;
}
.section {
  min-height: 400px;
  width: 100%;
  margin-top: 200px;
}
</style>
