<template>
  <div ref="container" class="container">
    <section ref="section1" class="section1" data-bgcolor="#bcb8ad" data-textcolor="#032f35">
      <div ref="logoRef" class="logo"></div>
    </section>
    <section ref="section2" class="section2">
      <div class="border">
        <svg
          viewBox="0 0 96 850"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
          class="divider-svg"
          data-v-d2ba1143=""
        >
          <path
            d="M1.00005 4.13072e-06L1.00004 211.531C1.00004 246.385 18.8257 278.818 48.25 297.5V297.5C77.6743 316.182 95.5 348.615 95.5 383.469L95.5 611.5"
            stroke="currentcolor"
          ></path>
        </svg>
      </div>
      <div class="section2__descriptions">
        <ul>
          <li ref="sec2Title">MEET ALEPH</li>
        </ul>
        <h2 ref="sec2Text">
          There are many variations of passages of Lorem Ipsum available, but the majority have
          suffered alteration in some form, by injected humour, or randomised words which don't look
          even slightly believable.
        </h2>
      </div>
    </section>
    <section ref="section" class="section3" data-bgcolor="#eacbd1" data-textcolor="#536fae">
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
    <section ref="section" class="section" data-bgcolor="#eacbd1" data-textcolor="#536fae">
      <h1 ref="secTitle">MEET ALEPH</h1>
      <h2 ref="secText">Lorem ipsum dolor sit amet, consectetur adipiscing elit.</h2>
    </section>
    <section ref="section" class="section" data-bgcolor="#eacbd1" data-textcolor="#536fae">
      <h1 ref="secTitle">MEET ALEPH</h1>
      <h2 ref="secText">Lorem ipsum dolor sit amet, consectetur adipiscing elit.</h2>
    </section>
    <div ref="backgroundRef" class="background"></div>
  </div>
</template>

<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
import * as THREE from 'three'

const logoRef = ref(null)
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
  const section2 = document.querySelectorAll('.section2')
  section2.forEach((el, index) => {
    gsap.fromTo(
      el,
      { opacity: 1, y: 0 },
      {
        opacity: 1,
        y: -200,
        duration: 1,
        delay: index,
        ease: 'power2.out',
        scrollTrigger: {
          trigger: el,
          start: 'top 90%',
          scrub: true, // ✅ حالا موقع اسکرول بالا و پایین کار می‌کنه
          toggleActions: 'restart pause resume reverse',
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
  width: 70%;
  height: 70%;
}
.border {
  width: 50%;
  height: 700px;
  display: flex;
  justify-content: flex-end;
}
.divider-svg {
  color: #000;
  opacity: 0.3;
  mask-image: linear-gradient(180deg, #000 0, #000 55%, #000000 100%);
  width: 90px;
  height: 100%;
}

.section2 {
  height: 100vh;
  width: 100%;
  display: flex;

  &__descriptions {
    width: 30%;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: flex-start;
    & > ul {
      padding: 0;
      > li {
        color: #26337f;
        font-size: 12px;
        height: 50px;
        font-weight: 600;
        padding: 0;
        list-style-type: disc;
        &::marker {
          color: #96f0fc;
          font-size: 20px;
        }
      }
    }
    & > h2 {
      color: #26337f;
      font-size: 20px;
      font-weight: 500;
      text-align: justify;
    }
  }
}
.section3 {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100%;
  color: #26337f;
  gap: 12px;
  transform: translate3d(0px, -159.091px, 0px);
  &__header {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    > span {
      font-size: 38px;
      font-weight: 400;
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
