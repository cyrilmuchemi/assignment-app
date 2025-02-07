<script setup>
import { ref } from 'vue'
import TodoList from './TodoList.vue'
const todoText = ref('')
const todos = ref([
  { id: 1, label: 'Build a rabbit cage', complete: false },
  { id: 2, label: ' Build an ecommerce website', complete: false },
  { id: 3, label: 'Be jacked as ***', complete: true },
  { id: 4, label: 'Own physical business', complete: true },
  { id: 5, label: 'Keep going', complete: false },
])

const addTodo = () => {
  if (todoText.value.trim()) {
    todos.value.push({
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
</script>

<template>
  <main id="body">
    <section id="hero">
      <header id="header">
        <nav id="navigation">
          <div><h1>TODO</h1></div>
          <div><img id="hero-img" src="../assets/images/icon-moon.svg" /></div>
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
      <TodoList :todos="todos" @toggle-complete="toggleComplete" @remove-todo="removeTodo" />
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
  background-image: url('../assets/images/bg-desktop-light.jpg');
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
</style>
