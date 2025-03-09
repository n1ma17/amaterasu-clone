<template>
  <div ref="container" class="container">
    <section ref="section1" class="section1" data-bgcolor="#bcb8ad" data-textcolor="#032f35">
      <h1>Change background color with GSAP ScrollTrigger</h1>
      <img
        src="https://images.pexels.com/photos/3062948/pexels-photo-3062948.jpeg?auto=compress&cs=tinysrgb&dpr=1&w=500"
        alt=""
      />
      <h2>Lorem ipsum dolor sit amet, consectetur adipiscing elit.</h2>
    </section>
    <section ref="section2" class="section2" data-bgcolor="#eacbd1" data-textcolor="#536fae">
      <h1>Change background color with GSAP ScrollTrigger</h1>
      <img
        src="https://images.pexels.com/photos/4467879/pexels-photo-4467879.jpeg?auto=compress&cs=tinysrgb&dpr=1&w=500"
        alt=""
      />
      <h2>Lorem ipsum dolor sit amet, consectetur adipiscing elit.</h2>
    </section>

    <section ref="section3" class="section3" data-bgcolor="#536fae" data-textcolor="#eacbd1">
      <h1>Change background color with GSAP ScrollTrigger</h1>
      <img
        src="https://images.pexels.com/photos/5604966/pexels-photo-5604966.jpeg?auto=compress&cs=tinysrgb&dpr=1&w=500"
        alt=""
      />
      <h2>Lorem ipsum dolor sit amet, consectetur adipiscing elit.</h2>
    </section>
    <section ref="section4" class="section4" data-bgcolor="#e3857a" data-textcolor="#f1dba7">
      <h1>Change background color with GSAP ScrollTrigger</h1>
      <img
        src="https://images.pexels.com/photos/4791474/pexels-photo-4791474.jpeg?auto=compress&cs=tinysrgb&dpr=1&w=500"
        alt=""
      />
      <h2>Lorem ipsum dolor sit amet, consectetur adipiscing elit.</h2>
    </section>
  </div>
</template>

<script setup>
import { onMounted } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

onMounted(() => {
  const sections = document.querySelectorAll('section')

  sections.forEach((section, index) => {
    gsap.fromTo(
      section,
      { opacity: 0, y: 10 },
      {
        opacity: 1,
        y: 0,
        duration: 2.5,
        delay: index * 0.5,
        ease: 'power2.out',
        scrollTrigger: {
          trigger: section,
          start: 'top 60%',
          end: 'top 20%',
          scrub: true, // ✅ وابسته به اسکرول
          toggleActions: 'restart pause resume reverse', // ✅ انیمیشن موقع اسکرول به بالا و پایین اجرا بشه
        },
      },
    )

    const elements = section.querySelectorAll('h1, img')

    elements.forEach((el, index) => {
      gsap.fromTo(
        el,
        { opacity: 0, y: 300 },
        {
          opacity: 1,
          y: 0,
          duration: 1,
          delay: index * 0.3,
          ease: 'power2.out',
          scrollTrigger: {
            trigger: section,
            start: 'top 80%',
            scrub: true, // ✅ حالا موقع اسکرول بالا و پایین کار می‌کنه
            toggleActions: 'restart pause resume reverse',
          },
        },
      )
    })
  })
})
</script>

<style lang="scss" scoped>
body {
  font-family: termina, sans-serif;
  transition: 0.3s ease-out;
}

.container {
  width: 100%;
  height: 100vh;
}

section {
  min-height: 100vh;
  width: 100%;
  position: relative;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  grid-gap: 2rem;
  padding: 50px 10vw;
  max-width: 1000px;
  margin: auto;
  place-items: center;
}

img {
  max-height: 80vh;
  width: 100%;
  object-fit: contain;
}

h1 {
  display: flex;
  font-size: 4rem;
  z-index: 2;
  line-height: 1.2;
  font-weight: 700;
}
h2 {
  font-size: 2rem;
  max-width: 400px;
}
.section1 {
  background-color: #fff;
  color: #536fae;
}
.section2 {
  background-color: #BFEEF5;
  color: #e3857a;
}
.section3 {
  background-color: #BFEEF5;
  color: #f1dba7;
}
.section4 {
  background-color: #BFEEF5;
  color: #eacbd1;
}
</style>
