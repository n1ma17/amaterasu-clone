<template>
  <div class="first_step">
    <div class="first_step__wrapper">
      <div ref="squareCircles" class="first_step__square">
        <SquareCircles :show-element="showElement" type="square" />
      </div>
      <div ref="dimondCircles" class="first_step__dimond">
        <SquareCircles :show-element="showElement" type="dimond" />
      </div>
      <div :class="!showElement ? 'circle-width' : ''" class="first_step__center-circle">
        <span>CLICK TO ENTER</span>
      </div>
    </div>
  </div>
</template>

<script setup>
import SquareCircles from '@/components/FirstStep/SquareCircles.vue'
import { onMounted, ref } from 'vue'
const showElement = ref(false)
onMounted(() => {
  setTimeout(() => {
    showElement.value = true
  }, 500)
})
</script>

<style lang="scss" scoped>
.circle-width {
  width: 250px !important;
  height: 250px !important;
}
.first_step {
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
  overflow: hidden;
  &__center-circle {
    width: 350px;
    height: 350px;
    border-radius: 50%;
    border: 1px solid #fff;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    transition: all 0.6s ease-in-out;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    > span {
      color: #fff;
      font-size: 12px;
      font-weight: 600;
    }
    &:hover {
      box-shadow:
        0px 0px 10px 0px #e2e9b9,
        inset 0px 0px 6px 0px #e2e9b9;
      transition: all 0.6s ease-in-out;
      width: 320px;
      height: 320px;
    }
    @media screen and (max-width: 768px) {
      width: 250px;
      height: 250px;
      &:hover {
        width: 220px;
        height: 220px;
      }
    }
    @media screen and (max-width: 520px) {
      width: 150px;
      height: 150px;
      &:hover {
        width: 120px;
        height: 120px;
      }
      > span {
        font-size: 10px;
      }
    }

  }
}

.first_step__wrapper {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.first_step__square,
.first_step__dimond {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.first_step__square {
  width: 500px;
  height: 500px;

  @media screen and (max-width: 768px) {
    width: 400px;
    height: 400px;
  }
  @media screen and (max-width: 520px) {
    width: 200px;
    height: 200px;
  }
}

.first_step__dimond {
  width: 650px;
  height: 650px;
  @media screen and (max-width: 768px) {
    width: 500px;
    height: 500px;
  }
  @media screen and (max-width: 520px) {
    width: 250px;
    height: 250px;
  }
}
</style>
