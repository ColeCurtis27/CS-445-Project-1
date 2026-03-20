<script setup>
import { ref } from 'vue'

import Home from './components/Home.vue'
import SmallPrompt from './components/SmallPrompt.vue'
import LargePrompt from './components/LargePrompt.vue'
import ImagePrompt from './components/ImagePrompt.vue'

const currentPage = ref('Home')
const bottles = ref([])

const bottleAmounts = {
  Small: 5,
  Large: 10,
  Image: 20
}

function goToPage(pageName) {
  currentPage.value = pageName

  const amount = bottleAmounts[pageName]

  for (let i = 0; i < amount; i++) {
    bottles.value.push({})
  }
}
</script>

<template>
  <div>

    <h1>Simulate Water Waste with ChatGPT</h1>

    <div>
      <Button label="Small Text Prompt" @click="goToPage('Small')"style="margin-right: 10px;" />
      <Button label="Large Text Prompt" @click="goToPage('Large')"style="margin-right: 10px;" />
      <Button label="Image Prompt" @click="goToPage('Image')" />
    </div>

    <Home v-if="currentPage === 'Home'" />
    <SmallPrompt v-if="currentPage === 'Small'" />
    <LargePrompt v-if="currentPage === 'Large'" />
    <ImagePrompt v-if="currentPage === 'Image'" />

    <div>
      <img
        v-for="(bottle, index) in bottles"
        :key="index"
        src="/bottle.png"
        width="59"
      />
    </div>
  </div>
</template>