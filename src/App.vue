<script setup>
import { ref, watch } from 'vue'
import TodoApp from './components/TodoApp.vue'
const darkMode = ref(false)
watch(darkMode, (newVal) => {
  document.body.classList.toggle('dark-mode', newVal)
})
const toggleTheme = () => {
  darkMode.value = !darkMode.value
}
</script>

<template>
  <div>
    <TodoApp :dark-mode="darkMode" @toggle-theme="toggleTheme" />
  </div>
</template>

<style>
.dark-mode {
  background-color: black;
  color: white;
}
</style>
