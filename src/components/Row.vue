<template>
  <div :class="`row ${first ? 'first' : ''}`" style="display: flex; flex: 1">
    <div class="cell" :style="getStyle(letters[0], 0)">
      {{ letters[0] ?? '' }}
    </div>
    <div class="cell" :style="getStyle(letters[1], 1)">
      {{ letters[1] ?? '' }}
    </div>
    <div class="cell" :style="getStyle(letters[2], 2)">
      {{ letters[2] ?? '' }}
    </div>
    <div class="cell" style="" :style="getStyle(letters[3], 3)">
      {{ letters[3] ?? '' }}
    </div>
    <div class="cell" :style="getStyle(letters[4], 4)">
      {{ letters[4] ?? '' }}
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  word: String,
  mainWord: Array,
  first: Boolean,
})

const letters = computed(() => props.word?.split('') ?? [])

const getStyle = (letter, index) => {
  if (!letter) return

  if (letter === props.mainWord[index]) {
    return {
      'background-color': '#00800091',
    }
  } else if (props.mainWord.includes(letter)) {
    return {
      'background-color': '#ffff0094',
    }
  }
}
</script>

<style scoped>
.row {
  --border-color: #172028;
  border-left: 2px solid var(--border-color);
}

.row.first {
  border-top: 2px solid var(--border-color);
}

.cell {
  border-right: 2px solid var(--border-color);
  border-bottom: 2px solid var(--border-color);
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 30px;
}
</style>
