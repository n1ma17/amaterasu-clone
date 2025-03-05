<template>
  <div class="first_step">
    <div class="first_step__wrapper">
      <div ref="squareCircles" class="first_step__square">
        <SquareCircles :show-element="showElement" type="square" />
      </div>
      <div ref="dimondCircles" class="first_step__dimond">
        <SquareCircles :show-element="showElement" type="dimond" />
      </div>
      <div v-if="showElement" class="first_step__center-circle">
        <span>click to enter</span>
      </div>
      <div v-else class="loader"></div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import SquareCircles from '@/components/FirstStep/SquareCircles.vue'

const showElement = ref(false)

onMounted(() => {
  setTimeout(() => {
    showElement.value = true
  }, 2500)
})
</script>

<style lang="scss" scoped>
.loader {
  width: 300px;
  height: 300px;
  border-radius: 50%;
  position: relative;
  animation: rotate 1s linear infinite;
}
.loader::before {
  content: '';
  box-sizing: border-box;
  position: absolute;
  inset: 0px;
  border-radius: 50%;
  border: 1px solid #fff;
  animation: prixClipFix 2.5s linear normal;
}

@keyframes rotate {
  100% {
    transform: rotate(360deg);
  }
}

@keyframes prixClipFix {
  0% {
    clip-path: polygon(50% 50%, 0 0, 0 0, 0 0, 0 0, 0 0);
  }
  25% {
    clip-path: polygon(50% 50%, 0 0, 100% 0, 100% 0, 100% 0, 100% 0);
  }
  50% {
    clip-path: polygon(50% 50%, 0 0, 100% 0, 100% 100%, 100% 100%, 100% 100%);
  }
  75% {
    clip-path: polygon(50% 50%, 0 0, 100% 0, 100% 100%, 0 100%, 0 100%);
  }
  100% {
    clip-path: polygon(50% 50%, 0 0, 100% 0, 100% 100%, 0 100%, 0 0);
  }
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
    width: 300px;
    height: 300px;
    border-radius: 50%;
    border: 1px solid #fff;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    transition: all 0.8s ease-in-out;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    @media screen and (max-width: 768px) {
      width: 250px;
      height: 250px;
      &:hover {
        width: 240px;
        height: 240px;
      }
    }
    @media screen and (max-width: 520px) {
      width: 150px;
      height: 150px;
      &:hover {
        width: 140px;
        height: 140px;
      }
    }
    span {
      color: #fff;
      font-size: 16px;
      font-weight: 600;
      @media screen and (max-width: 768px) {
        font-size: 12px;
      }
      @media screen and (max-width: 520px) {
        font-size: 10px;
      }
    }
    &:hover {
      box-shadow:
        inset 1px 1px 8px 0px #898787,
        1px 1px 20px 0px #898787;
      width: 280px;
      height: 280px;
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
