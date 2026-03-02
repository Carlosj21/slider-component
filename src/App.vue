<template>
  <Slider :imageUrls="imageUrls" />
</template>
<script setup lang="ts">
import Slider from './components/Slider/Slider.vue'
import slide1 from '@/assets/img1.png'
import slide2 from '@/assets/img2.png'
import slide3 from '@/assets/img3.png'
import slide4 from '@/assets/img4.png'

const imageUrls = [
  slide1,
  slide2,
  slide3,
  slide4
]
</script>
<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}

.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
