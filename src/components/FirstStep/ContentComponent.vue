<!--
<template>
  <div class="first_step">
    <div class="first_step__wrapper">
      <div ref="squareCircles" class="first_step__square">
        <SquareCircles :show-element="showElement" type="square" />
      </div>
      <div ref="dimondCircles" class="first_step__dimond">
        <SquareCircles :show-element="showElement" type="dimond" />
      </div>

      <div :style="progressStyle">
        <svg class="progress-circle" viewBox="0 0 100 100">
          <circle
            class="progress"
            cx="50"
            cy="50"
            r="50"
            stroke-width="0.5"
            :style="{ strokeDashoffset }"
            :class="{ 'is-complete': progress.value === 100 }"
          ></circle>
        </svg>
      </div>
    </div>
  </div>
</template> -->
<template>
  <div class="first_step">
    <div class="first_step__wrapper">
      <div ref="squareCircles" class="first_step__square">
        <SquareCircles :show-element="showElement" type="square" />
      </div>
      <div ref="dimondCircles" class="first_step__dimond">
        <SquareCircles :show-element="showElement" type="dimond" />
      </div>

      <!-- Animated transition wrapper -->
      <div :style="progressStyle">
        <svg class="progress-circle" viewBox="0 0 100 100">
          <circle
            class="progress"
            cx="50"
            cy="50"
            r="50"
            stroke-width="0.5"
            :style="{ strokeDashoffset }"
          ></circle>
        </svg>

        <!-- Text in the center of the circle -->
        <div v-if="progress === 100" class="center-text">
          <span>click to enter</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue'
import SquareCircles from '@/components/FirstStep/SquareCircles.vue'

const showElement = ref(false)
const progress = ref(0) // Start at 0%

const circumference = 2 * Math.PI * 45 // Circle path calculation
const strokeDashoffset = computed(() => {
  return circumference - (circumference * progress.value) / 100
})

// Animate progress
const animateProgress = (duration) => {
  const startTime = performance.now()

  const step = (currentTime) => {
    const elapsedTime = currentTime - startTime
    const progressValue = Math.min((elapsedTime / duration) * 100, 100)

    progress.value = progressValue

    if (progressValue < 100) {
      requestAnimationFrame(step)
    } else {
      // When progress reaches 100%, complete the circle
      setTimeout(() => {
        showElement.value = true // Show text after animation ends
      }, 500) // Small delay for smooth transition
    }
  }

  requestAnimationFrame(step)
}

onMounted(() => {
  animateProgress(3000) // 3 seconds animation
})

// Style to animate center circle growth
const progressStyle = computed(() => ({
  width: '100vw',
  height: '100vh',
  display: 'flex',
  alignItems: 'center',
  justifyContent: 'center',
}))
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
}

/* Circular Progress Styles */
.progress-circle {
  width: 350px;
  height: 350px;
  transition: all 0.1s ease-in-out;
}

circle {
  fill: none;
  stroke-width: 1;
  stroke-linecap: round;
  transform: rotate(-90deg);
  transform-origin: center;
}

.progress {
  stroke-width: 0.4; /* Makes it thinner */
  stroke: #fff;
  stroke-dasharray: 314; /* Full circumference of the circle (2 * PI * 50) */
  stroke-dashoffset: 314; /* Start at full offset */
  transition: stroke-dashoffset 0.1s ease-out;
}

/* When the circle is complete, add a fill */
.progress.is-complete {
  stroke: #4caf50; /* Green when complete */
  fill: #4caf50; /* Fill circle with green */
  stroke-dashoffset: 0; /* Complete the stroke */
}

/* Text in the center when progress is 100% */
.center-text {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  color: #fff;
  font-size: 20px;
  font-weight: 600;
  text-align: center;
  transition: opacity 0.3s ease-in-out;
}

/* Keep your other elements untouched */
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
