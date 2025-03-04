<template>
  <div v-if="type === 'square'" ref="squareCircles" class="square">
    <div v-for="i in 4" :key="`square-circle-${i}`" ref="squareCircle" class="square__circle"></div>
  </div>
  <div v-else ref="dimondCircles" class="dimond">
    <div
      v-for="i in 4"
      :key="`dimond-circle-${i}`"
      ref="dimondCircle"
      class="dimond__circle"
    ></div>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue'

const props = defineProps({
  type: String,
  showElement: Boolean
});

const dimondCircles = ref(null)
const dimondCircle = ref([])
const squareCircles = ref(null)
const squareCircle = ref([])
watch(() => props.showElement, () => {
  if (props.type === 'square') {
    setSquareCircles()
  } else {
    setDimondCircles()
  }
})
const setDimondCircles = () => {
  if (!dimondCircles.value || dimondCircle.value.length !== 4) return
  dimondCircle.value.forEach((circle, index) => {
    circle.style.opacity = '1'
    switch (index) {
      case 0:
        circle.style.top = '0px'
        circle.style.left = '50%'
        circle.style.transform = 'translateX(-50%)'
        break
      case 1:
        circle.style.top = '100%'
        circle.style.left = '50%'
        circle.style.transform = 'translate(-50%, -100%)'
        break
      case 2:
        circle.style.top = '50%'
        circle.style.left = '0'
        circle.style.transform = 'translate(0, -50%)'
        break
      case 3:
        circle.style.top = '50%'
        circle.style.left = '100%'
        circle.style.transform = 'translate(-100%, -50%)'
        break
    }
  })
}

const setSquareCircles = () => {
  if (!squareCircles.value || squareCircle.value.length !== 4) return
  squareCircle.value.forEach((circle, index) => {
    circle.style.opacity = '1'
    switch (index) {
      case 0:
        circle.style.top = '0'
        circle.style.left = '0'
        circle.style.transform = 'translate(0, 0)'
        break
      case 1:
        circle.style.top = '100%'
        circle.style.left = '0'
        circle.style.transform = 'translate(0, -100%)'
        break
      case 2:
        circle.style.top = '0'
        circle.style.left = '100%'
        circle.style.transform = 'translate(-100%, 0)'
        break
      case 3:
        circle.style.top = '100%'
        circle.style.left = '100%'
        circle.style.transform = 'translate(-100%, -100%)'
        break
    }
  })
}

// onMounted(() => {
//   setTimeout(() => {
//     if (props.type === 'square') {
//       setSquareCircles()
//     } else {
//       setDimondCircles()
//     }
//   }, 500)
// })
</script>

<style lang="scss" scoped>
.square {
  width: 100%;
  height: 100%;
  &__circle {
    opacity: 0;
    width: 250px;
    height: 250px;
    border-radius: 50%;
    border: 1px solid #ffffff65;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    transition: all 0.8s ease-in-out;
  }
  @media screen and (max-width: 768px) {
    &__circle {
      width: 200px;
      height: 200px;
    }
  }
  @media screen and (max-width: 520px) {
    &__circle {
      width: 100px;
      height: 100px;
    }
  }
}

.dimond {
  width: 100%;
  height: 100%;
  &__circle {
    opacity: 0;
    width: 250px;
    height: 250px;
    border-radius: 50%;
    border: 1px solid #ffffff65;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    transition: all 0.8s ease-in-out;
    padding: 20px;
  }
  @media screen and (max-width: 768px) {
    &__circle {
      width: 200px;
      height: 200px;
    }
  }
  @media screen and (max-width: 520px) {
    &__circle {
      width: 100px;
      height: 100px;
    }
  }
}
</style>
