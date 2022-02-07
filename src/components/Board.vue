<template>
  <div class="board" style="">
    <Row
      v-for="index of [0, 1, 2, 3, 4]"
      :key="index"
      :word="words[index]"
      :mainWord="splitWord"
      :first="index === 0"
    >
    </Row>
  </div>
  <input
    ref="input"
    class="input"
    v-model="newWord"
    @keyup.enter="handleGuess"
    maxlength="5"
  />
  <Alphabet :guesses="guesses" />
</template>

<script setup>
import { ref, computed, watch } from 'vue'
import Alphabet from './Alphabet.vue'
import Row from './Row.vue'

const props = defineProps({
  word: String,
})

const splitWord = computed(() => props.word.split(''))
const words = ref([])
const newWord = ref('')
const guesses = computed(() => [...new Set(words.value.join())])
const input = ref()

const handleGuess = () => {
  words.value = [...words.value, newWord.value.toLowerCase()]
  newWord.value = ''
}

watch(input, () => {
  input.value?.focus()
})
</script>

<style scoped>
.board {
  width: 500px;
  height: 500px;
  display: flex;
  flex-direction: column;
}

.input {
  margin: 18px 0 12px;
  padding: 6px;
  display: inline-block;
  border-radius: 4px;
  box-sizing: border-box;
  background-color: antiquewhite;
  border: 0;
}
</style>
