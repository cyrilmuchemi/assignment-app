<script setup>
import { ref, watch, computed, onMounted } from 'vue'
import TodoList from './TodoList.vue'
import moonIcon from '@/assets/images/icon-moon.svg'
import sunIcon from '@/assets/images/icon-sun.svg'
import lightHero from '@/assets/images/bg-desktop-light.jpg'
import darkHero from '@/assets/images/bg-desktop-dark.jpg'

const props = defineProps({
  darkMode: Boolean,
})

const loadTodos = () => {
  const savedTodos = localStorage.getItem('todos')
  return savedTodos
    ? JSON.parse(savedTodos).sort((a, b) => b.id - a.id)
    : [{ id: 1, label: 'Add a new todo', complete: false }]
}

const todoText = ref('')

const todos = ref(loadTodos)

watch(
  todos,
  (newTodos) => {
    todos.value.sort((a, b) => b.id - a.id)
    localStorage.setItem('todos', JSON.stringify(newTodos))
  },
  { deep: true },
)

const addTodo = () => {
  if (todoText.value.trim()) {
    todos.value.unshift({
      id: todos.value.length + 1,
      label: todoText.value,
      complete: false,
    })
    todoText.value = ''
  }
}

const removeTodo = (todoId) => {
  todos.value = todos.value.filter((todo) => todo.id !== todoId)
}

const toggleComplete = (todoId) => {
  const todo = todos.value.find((todo) => todo.id === todoId)
  if (todo) {
    todo.complete = !todo.complete
  }
}

onMounted(() => {
  todos.value = loadTodos()
})

const heroStyle = computed(() => ({
  backgroundImage: `url(${props.darkMode ? darkHero : lightHero})`,
}))
</script>

<template>
  <main id="body">
    <section id="hero" :style="heroStyle">
      <header id="header">
        <nav id="navigation">
          <div><h1>TODO</h1></div>
          <div class="toggle-img" @click="$emit('toggle-theme')">
            <img :src="darkMode ? sunIcon : moonIcon" />
          </div>
        </nav>
      </header>
      <div>
        <form @submit.prevent="addTodo">
          <label>
            <input
              id="todo-input"
              v-model="todoText"
              placeholder="Create a new todo.."
              type="text"
            />
          </label>
        </form>
      </div>
    </section>
    <section id="list">
      <TodoList
        :todos="todos"
        :dark-mode="darkMode"
        @toggle-complete="toggleComplete"
        @remove-todo="removeTodo"
      />
    </section>
    <section id="footer"></section>
  </main>
</template>

<style scoped>
#body {
  width: 100%;
  box-sizing: border-box;
}

#header {
  display: flex;
  align-items: center;
  justify-content: center;
}

#hero {
  background-size: cover;
  background-repeat: no-repeat;
  height: 50vh;
  text-align: center;
}

#navigation {
  display: flex;
  align-items: center;
  gap: 250px;
}

h1 {
  font-size: 50px;
  color: #fff;
  letter-spacing: 1.5rem;
}

#todo-input {
  width: 33%;
  height: 50px;
  border-radius: 8px;
  border: #fff;
}

input::placeholder {
  padding-left: 30px;
}

.toggle-img {
  cursor: pointer;
}
</style>
