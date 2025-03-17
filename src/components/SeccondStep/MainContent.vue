<template>
  <div ref="container" class="container">
    <section ref="section1" class="section1" data-bgcolor="#bcb8ad" data-textcolor="#032f35">
      <div ref="logoRef" class="logo"></div>
    </section>
    <section ref="section2" class="section2">
      <div class="border">
        <svg
          viewBox="0 0 100 450"
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
    <section ref="section4" class="section4" data-bgcolor="#eacbd1" data-textcolor="#536fae">
      <div ref="oval3" class="oval-front">
        How do you balance your personal ambitions with maintaining relationships?
      </div>
      <div class="background-ovals">
        <div ref="oval1" class="oval1 oval-bg">
          How do you balance your personal ambitions with maintaining relationships?
        </div>
        <div ref="oval2" class="oval2 oval-bg">
          How do you balance your personal ambitions with maintaining relationships?
        </div>
      </div>
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

const oval1 = ref(null)
const oval2 = ref(null)
const oval3 = ref(null)

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
  const ovals = [oval1.value, oval2.value]
  window.addEventListener('mousemove', (event) => {
    const { clientX: x, clientY: y } = event
    const centerX = window.innerWidth / 2
    const centerY = window.innerHeight / 2

    ovals.forEach((oval, index) => {
      const intensity = index === 2 ? 1.5 : 1 // بیضی جلوتر سریع‌تر حرکت کنه
      const moveX = (x - centerX) / 30 * intensity
      const moveY = (y - centerY) / 30 * intensity
      gsap.to(oval, {
        x: moveX,
        y: moveY,

        duration: 0.4,
        ease: 'power2.out'
      })
    })
  })
  window.addEventListener('mousemove', (event) => {
    const { clientX: x, clientY: y } = event
    const centerX = window.innerWidth / 2
    const centerY = window.innerHeight / 2

    const intensity = 1
    const moveX = -(x - centerX) / 100 * intensity
    const moveY = -(y - centerY) / 100 * intensity
    gsap.to(oval3.value, {
        x: moveX,
        y: moveY,

        duration: 0.4,
        ease: 'power2.out'
      })
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
  width: 50%;
  height: 50%;
}
.border {
  width: 50%;
  height: 400px;
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
  height: fit-content;
  width: 100%;
  max-height: 400px;
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

.section4 {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100vh;
  overflow: hidden;
}

.background-ovals {
  position: absolute;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  right: 0;
  left: 0;
  margin: auto;
  filter: blur(3px);

}
.oval2 {
  position: absolute;
  width: 320px; /* اندازه بیضی */
  height: 120px;
  right: 10%;
  top: 50%;
  border-radius: 100px;
  border: 1px solid rgba(63, 63, 63, 0.986);
  transition: transform 0.2s ease-out;
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  padding: 16px;
}
.oval1 {
  position: absolute;
  width: 300px; /* اندازه بیضی */
  height: 100px;
  right: 40%;
  top: 25%;
  border-radius: 100px;
  border: 1px solid rgba(134, 134, 134, 0.801);
  transition: transform 0.2s ease-out;
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  padding: 16px;
}

.oval-bg {
  opacity: 0.3; /* محو کردن بیضی‌های پس‌زمینه */
}

.oval-front {
  position: absolute;
  right: 50%;
  border-radius: 100px;
  border: 1px solid rgba(173, 173, 173, 0.664);
  transition: transform 0.2s ease-out;
  opacity: 1;
  color: rgba(38, 51, 127, 1);
  font-size: 16px;
  width: 400px; /* اندازه بیضی */
  height: 150px;
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  padding: 16px;
}

</style>
