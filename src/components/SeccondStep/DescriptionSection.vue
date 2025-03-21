<template>
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
</template>

<script setup>
import { gsap } from 'gsap'
import { onMounted } from 'vue'

onMounted(() => {
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
})
</script>

<style lang="scss" scoped>
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
</style>
