<script setup>
import { ref } from 'vue'
import TodoList from './TodoList.vue'
const todo = ref('')
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
        <label>
          <input id="todo-input" v-model="todo" placeholder="Create a new todo.." type="text" />
        </label>
      </div>
    </section>
    <section id="list">
      <TodoList />
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
