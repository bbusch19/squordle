<template>
  <div class="wrapper">
    <div
      class="alphabet"
      v-for="letter in alphabet"
      :key="letter"
      :style="{
        'background-color': guesses.includes(letter) ? 'gray' : 'transparent',
      }"
    >
      {{ letter }}
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  guesses: Array,
})

const alphabet = 'abcdefghijklmnopqrstuvwxyz'.split('')
</script>

<style scoped>
.wrapper {
  display: flex;
  justify-content: center;
  gap: 6px;
}

.alphabet {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 24px;
  height: 24px;
  text-align: center;
  border-radius: 2px;
  font-size: 18px;
}
</style>
