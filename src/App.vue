<template>
  <h1>SQUORDLE</h1>
  <Board v-if="word" :word="word" />
  <div v-else>...loading</div>
</template>

<script setup>
import { onMounted, ref } from '@vue/runtime-core'
import Board from './components/Board.vue'
import axios from 'axios'

const word = ref('')
const options = {
  method: 'GET',
  url: 'https://wordsapiv1.p.rapidapi.com/words/',
  params: {
    random: 'true',
    lettersMax: 5,
    lettersMin: 5,
    frequencyMin: 4.5,
  },
  headers: {
    'x-rapidapi-host': 'wordsapiv1.p.rapidapi.com',
    'x-rapidapi-key': process.env.VUE_APP_API_KEY,
  },
}

onMounted(async () => {
  const response = await axios.request(options)
  word.value = response.data.word
})
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: antiquewhite;
  margin-top: 60px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

body {
  background-color: #2c3e50;
}
</style>
