<template>
  <section ref="section5" class="section5">
    <div class="section5__content">
      <div class="section5__content__header">
        <span> Chaos </span>
        <span> Order </span>
      </div>
      <span class="section5__content__text">
        We apply non-linear dynamics to capture the complex chaos within you.
      </span>
    </div>
    <div ref="threeContainer" class="three-container"></div>
  </section>
</template>

<script setup>
import { onMounted, ref } from 'vue'

import * as THREE from 'three'
import { OBJLoader } from 'three/examples/jsm/loaders/OBJLoader'
import { gsap } from 'gsap'

const threeContainer = ref(null)
let model = null // برای ذخیره مدل سه‌بعدی
const initThree = function () {
  // گرفتن اندازه سه‌کانتینر
  const containerWidth = threeContainer.value.offsetWidth
  const containerHeight = threeContainer.value.offsetHeight

  // صحنه و دوربین و رندر
  const scene = new THREE.Scene()
  const camera = new THREE.PerspectiveCamera(
    45,
    containerWidth / containerHeight, // نسبت تصویر بر اساس ابعاد کانتینر
    1,
    1000,
  )

  const renderer = new THREE.WebGLRenderer({ alpha: true }) // افزودن transparency
  renderer.setSize(containerWidth, containerHeight) // تنظیم اندازه رندرر
  renderer.setPixelRatio(window.devicePixelRatio) // پشتیبانی از نمایشگرهای با کیفیت بالا
  threeContainer.value.appendChild(renderer.domElement)

  // Loader برای مدل OBJ
  const loader = new OBJLoader()

  // لود کردن مدل
  loader.load(
    '/models/model3.obj',
    (object) => {
      object.position.set(0, -1.5, 0) // مرکز مدل
      object.scale.set(0.07, 0.07, 0.07)
      object.rotation.y = Math.PI / 2
      scene.add(object)
      model = object // ذخیره مدل برای تغییرات
      let targetRotationX = 0 // مقدار هدف برای چرخش در محور X
      let targetRotationY = Math.PI / 4 // مقدار هدف برای چرخش در محور Y (حفظ ۹۰ درجه)
      let targetRotationZ = 0 // مقدار هدف برای چرخش در محور Z

      let currentRotationX = 0 // مقدار فعلی چرخش در محور X
      let currentRotationY = Math.PI / 4 // مقدار فعلی چرخش در محور Y
      let currentRotationZ = 0 // مقدار فعلی چرخش در محور Z

      const rotationSpeed = 0.02 // سرعت چرخش برای حرکت نرم

      // تابع برای بروزرسانی چرخش مدل به صورت تدریجی
      function updateRotation() {
        currentRotationX += (targetRotationX - currentRotationX) * rotationSpeed
        currentRotationY += (targetRotationY - currentRotationY) * rotationSpeed
        currentRotationZ += (targetRotationZ - currentRotationZ) * rotationSpeed

        // به‌روزرسانی چرخش مدل
        model.rotation.x = currentRotationX
        model.rotation.y = currentRotationY
        model.rotation.z = currentRotationZ

        // درخواست انیمیشن برای فریم بعدی
        requestAnimationFrame(updateRotation)
      }

      // فراخوانی اولیه تابع انیمیشن
      updateRotation()

      // اضافه کردن رویداد mousemove به document برای چرخش مدل
      document.addEventListener('mousemove', (event) => {
        // محاسبه موقعیت موس نسبت به اندازه صفحه
        const mouseX = (event.clientX / window.innerWidth) * 2 - 1 // موقعیت موس در محور X
        const mouseY = -(event.clientY / window.innerHeight) * 2 + 1 // موقعیت موس در محور Y

        // تغییر مقدار هدف چرخش در محورهای مختلف
        targetRotationX = (mouseY * Math.PI) / 32 // چرخش مدل در محور X
        targetRotationZ = (mouseX * Math.PI) / 100 // چرخش مدل در محور Z

        // حفظ مقدار ۹۰ درجه برای محور Y و تغییر کمی بر اساس حرکت موس
        targetRotationY = Math.PI / 4 + (mouseX * Math.PI) / 45 // چرخش خیلی کم در محور Y
      })

      // هنگامی که موس از روی مدل خارج می‌شود، رویداد mousemove را غیرفعال می‌کنیم
      model.addEventListener('mouseout', () => {
        document.removeEventListener('mousemove', () => {})
      })

      // افزودن نور
      const pointLight = new THREE.PointLight(0xffffff, 300)
      pointLight.position.set(10, 10, 10)
      scene.add(pointLight)
    },
    (xhr) => {
      console.log((xhr.loaded / xhr.total) * 100 + '% loaded')
    },
    (error) => {
      console.error('An error occurred while loading the OBJ model:', error)
    },
  )

  // تنظیم موقعیت دوربین
  camera.position.z = 5

  // حلقه انیمیشن برای رندر کردن صحنه
  function animate() {
    requestAnimationFrame(animate)
    renderer.render(scene, camera)
  }
  animate()

  // به‌روز کردن رندرر هنگام تغییر سایز پنجره
  window.addEventListener('resize', () => {
    const newWidth = threeContainer.value.offsetWidth
    const newHeight = threeContainer.value.offsetHeight
    renderer.setSize(newWidth, newHeight)
    camera.aspect = newWidth / newHeight
    camera.updateProjectionMatrix() // به‌روزرسانی ماتریس دوربین
  })
}
onMounted(() => {
  gsap.fromTo(
    '.three-container',
    { y: 400 },
    {
      opacity: 1,
      duration: 2,
      y: -250,
      scrollTrigger: {
        trigger: '.three-container',
        start: 'top 100%',
        end: 'top 40%',
        scrub: true,
        toggleActions: 'restart pause resume reverse',
      },
    }
  );

  gsap.fromTo(
    '.section5__content',
    { opacity: 0, y: 0 },
    {
      opacity: 1,
      duration: 1,
      delay: 0.5,
      y: 50,
      scrollTrigger: {
        trigger: '.section5__content',
        start: 'top 90%',
        end: 'top 40%',
        scrub: true,
        toggleActions: 'restart pause resume reverse',
      },
    }
  );
  gsap.fromTo(
    '.section5',
    { opacity: 0 },
    {
      opacity: 1,
      duration: 2,
      delay: 0.5,
      scrollTrigger: {
        trigger: '.section5',
        start: 'top 90%',
        end: 'top 40%',
        scrub: true,
        toggleActions: 'restart pause resume reverse',
      },
    },
  )
  initThree()
})
</script>

<style lang="scss" scoped>
.section5 {
  height: 100vh;
  opacity: 0;
  transition: opacity 1s ease-in-out;
  display: flex;
  align-items: center;
  padding: 0 80px;
  &__content {
    width: 400px;
    display: flex;
    flex-direction: column;
    color: #26337f;
    align-items: flex-start;
    justify-content: center;
    gap: 20px;
    &__header {
      display: flex;
      flex-direction: column;
      > span {
        font-size: 44px;
        font-weight: 700;
      }
    }
    > span {
      font-size: 24px;
      font-weight: 400;
    }
  }
}
.three-container {
  width: calc(100% - 560px);
  height: 100%;
}
</style>
