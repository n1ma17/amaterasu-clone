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
      <div v-else class="first_step__loader">
        <div class="loader"></div>
      </div>
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
  }, 3500)
})
</script>

<style lang="scss" scoped>


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
    border: 1px solid #ffffff65;
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
      color: #ffffff65;
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
        width: 340px;
        height: 340px;
    }
  }
  &__loader {
    width: 350px;
    height: 350px;
    .loader,.loader:before,.loader:after{
    top:0;
    bottom:0;
    left:0;
    right:0;
    content:"";
    position:absolute;
    border-radius:50%;
  }

  .loader{
    width:350px;
    height:350px;
    animation:spin 1s linear infinite;
  }

  @keyframes spin{
    100%{transform:rotate(360deg);}
  }

  .loader:before{
    border:1px solid #183969;
    border-bottom:1px solid #fff;
    border-left:1px solid #fff;
    animation:spin1 12s linear infinite;
  }

  .loader:after{
    border:1px solid #183969;
    border-top:1px solid transparent;
    border-right:1px solid transparent;
    animation:spin2 12s linear infinite;
  }

  @keyframes spin1{
    20%{transform:rotate(150deg)}
    40%{transform:rotate(300deg)}
    80%{transform:rotate(300deg)}
    100%{transform:rotate(360deg)}
  }

  @keyframes spin2{
    0%{transform:rotate(-30deg)}
    20%{transform:rotate(-30deg);
        border-color:transparent transparent #183969 #183969}
    21%{border-color:#fff #fff transparent transparent}
    40%{transform:rotate(-30deg)}
    60%{transform:rotate(120deg);
        border-color:#fff #fff transparent transparent}
    61%{border-color:transparent transparent #183969 #183969}
    80%{transform:rotate(270deg)}
    100%{transform:rotate(360deg);border-color:#fff #fff transparent transparent}
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
