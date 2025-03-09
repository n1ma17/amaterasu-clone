<template>
  <main>
    <RouterView />
    <div ref="flair" class="flair flair--3">
    </div>
    <div ref="dot" class="dot dot--3"></div>
  </main>
</template>

<script setup>
import { onMounted } from 'vue'
import { gsap } from 'gsap'
import { RouterView } from 'vue-router'
onMounted(() => {
  const flair = document.querySelector('.flair')
  gsap.set(flair, { xPercent: -50, yPercent: -50 })
  let xTo = gsap.quickTo(flair, 'x', { duration: 0.6, ease: 'power3' }),
    yTo = gsap.quickTo(flair, 'y', { duration: 0.6, ease: 'power3' })

  window.addEventListener('mousemove', (e) => {
    xTo(e.clientX)
    yTo(e.clientY)
  })
  const dot = document.querySelector('.dot')
  gsap.set(dot, { xPercent: -30, yPercent: -30 })
  let xPos = gsap.quickTo(dot, 'x', { duration: 0.9, ease: 'power3' }),
    yPos = gsap.quickTo(dot, 'y', { duration: 0.9, ease: 'power3' })

  window.addEventListener('mousemove', (e) => {
    xPos(e.clientX)
    yPos(e.clientY)
  })
})
</script>

<style scoped lang="scss">
.flair {
  width: 50px;
  height: 50px;
  position: fixed;
  top: 0;
  left: 0;
  pointer-events: none;
  border: 1px solid #c5c5c5;
  border-radius: 50%;
}
.dot {
  width: 5px;
  height: 5px;
  position: fixed;
  top: 0;
  left: 0;
  pointer-events: none;
  background-color: #7c7b7b;
  border-radius: 50%;
}
</style>
