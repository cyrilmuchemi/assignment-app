<script setup>
import { ref, watch, onMounted } from 'vue'
import TodoApp from './components/TodoApp.vue'
const darkMode = ref(false)
watch(darkMode, (newVal) => {
  document.body.classList.toggle('dark-mode', newVal)
})
const toggleTheme = () => {
  darkMode.value = !darkMode.value
}
onMounted(() => {
  const savedTheme = localStorage.getItem('darkMode')
  darkMode.value = savedTheme === 'true'
})
</script>

<template>
  <div>
    <TodoApp :dark-mode="darkMode" @toggle-theme="toggleTheme" />
  </div>
</template>

<style>
.dark-mode {
  background-color: #171823;
  color: white;
}
</style>
