<template>
  <section ref="section1" class="section1" data-bgcolor="#bcb8ad" data-textcolor="#032f35">
    <div ref="logoRef" class="logo"></div>
  </section>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'

const logoRef = ref(null)
onMounted(() => {
  const section1 = document.querySelectorAll('.section1')
  section1.forEach((section, index) => {
    gsap.fromTo(
      section,
      { opacity: 0, y: 0 },
      {
        opacity: 1,
        y: 10,
        duration: 9,
        delay: index,
        ease: 'power2.out',
        scrollTrigger: {
          trigger: section,
          start: 'top 100%',
          end: 'top 20%',
          scrub: true, // ✅ وابسته به اسکرول
          toggleActions: 'restart pause resume reverse', // ✅ انیمیشن موقع اسکرول به بالا و پایین اجرا بشه
        },
      },
    )
  })
  logoRef.value.addEventListener('mousemove', (event) => {
    const { width, height, left, top } = logoRef.value.getBoundingClientRect()
    const x = (event.clientX - left) / width - 0.5
    const y = (event.clientY - top) / height - 0.5

    const rotateX = y * 40
    const rotateY = -x * 40
    const depth = -250

    gsap.to(logoRef.value, {
      rotateX,
      rotateY,
      z: depth,
      duration: 0.9,
      delay: 1.5,
      ease: 'power2.out',
    })
  })

  logoRef.value.addEventListener('mouseleave', () => {
    gsap.to(logoRef.value, {
      rotateX: 0,
      rotateY: 0,
      z: 0,
      duration: 0.3,
      ease: 'power2.out',
    })
  })
})
</script>

<style lang="scss" scoped>
.section1 {
  height: calc(100vh - 50px);
  width: 100%;
  position: relative;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  grid-gap: 2rem;
  place-items: center;
}
.logo {
  background: linear-gradient(45deg, #fff 0, #b6ecf3 100%);
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  position: absolute;
  mask-image: url(../../assets/logo.svg);
  mask-repeat: no-repeat;
  mask-size: contain;
  mask-position: center;
  width: 50%;
  height: 50%;
}
</style>
