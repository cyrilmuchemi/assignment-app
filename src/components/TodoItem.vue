<script setup>
import { ref } from 'vue'
const todos = ref([
  { id: 1, label: 'Build a rabbit cage', complete: false },
  { id: 2, label: ' Build an ecommerce website', complete: false },
  { id: 3, label: 'Be jacked as ***', complete: true },
  { id: 4, label: 'Own physical business', complete: true },
  { id: 5, label: 'Keep going', complete: false },
])
const toggleComplete = (todo) => {
  todo.complete = !todo.complete
}
</script>
<template>
  <div class="todos">
    <ul>
      <li v-for="todo in todos" :key="todo.id" :class="{ strikeout: todo.complete }">
        <div class="task">
          <div class="checkbox">
            <label>
              <input v-model="todo.complete" type="checkbox" @click="toggleComplete(todo)" />
              <span></span>
            </label>
          </div>
          <div class="task-name">
            <p>{{ todo.label }}</p>
          </div>
        </div>
        <diV class="divider"></diV>
      </li>
    </ul>
  </div>
</template>
<style scoped>
label {
  position: relative;
}
span {
  width: 26px;
  height: 26px;
  border: 3px solid #8888;
  display: inline-block;
  border-radius: 50%;
  transition: all linear 0.3s;
  &:after {
    content: '';
    position: absolute;
    top: -5px;
    left: 10px;
    border-bottom: 2px solid #fff;
    border-right: 2px solid #fff;
    height: 9px;
    width: 4px;
    transform: rotate(45deg);
    visibility: hidden;
  }
}

input {
  display: none;
  &:checked ~ span {
    background: rgb(157, 82, 226);
    &:after {
      visibility: visible;
    }
  }
}

.divider {
  height: 2px;
  margin-left: -36px;
  background-color: gray;
}

.task {
  display: flex;
  align-items: center;
  gap: 15px;
}

ul {
  list-style: none;
}

.todos {
  margin: auto;
}

.strikeout {
  text-decoration: line-through;
}
</style>
