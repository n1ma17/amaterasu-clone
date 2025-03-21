<template>
  <section ref="section3" class="section3" data-bgcolor="#eacbd1" data-textcolor="#536fae">
    <div ref="sec3Title" class="section3__header">
      <span>Your Mind,</span>
      <span>Mapped</span>
    </div>
    <h2 ref="secText">
      We tirelessly work with our team of psychologists and neuroscientists to model a multi-modal
      intake mechanisms to understand the true you across varying degrees of abstraction, through
      exposure to art, music, games, and introspective questions.
    </h2>
  </section>
</template>

<script setup>
import { onMounted } from 'vue'
import { gsap } from 'gsap'
onMounted(() => {
  gsap.fromTo(
    '.section3__header',
    { opacity: 0.3, y: -50, filter: 'blur(10px)' },
    {
      opacity: 1,
      y: -100,
      filter: 'blur(0px)',
      duration: 1,
      ease: 'power2.out',
      scrollTrigger: {
        trigger: '.section3',
        start: 'top 100%',
        end: 'top 20%',
        scrub: true,
        toggleActions: 'restart pause resume reverse',
      },
    },
  )
})
</script>

<style lang="scss" scoped>
.section3 {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  width: 100%;
  height: 300px;
  color: #26337f;
  &__header {
    transform: translate3d(0px, -259.091px, 0px);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    > span {
      font-size: 4rem;
      font-weight: 400;
      line-height: 4rem;
      padding: 0;
    }
  }
  & > h2 {
    width: 40%;
    text-align: center;
    font-size: 16px;
  }
}
</style>
