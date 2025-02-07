<script setup>
import { defineProps, defineEmits } from 'vue'
const props = defineProps({
  todo: Object,
})
const emit = defineEmits(['toggle-complete', 'remove-todo'])
const toggleComplete = () => {
  emit('toggle-complete', props.todo.id)
}
const removeTodo = () => {
  emit('remove-todo', props.todo.id)
}
</script>
<template>
  <div class="todos">
    <ul>
      <li :class="{ strikeout: todo.complete }">
        <div class="task">
          <div class="checkbox">
            <label>
              <input type="checkbox" :checked="todo.complete" @change="toggleComplete" />
              <span></span>
            </label>
          </div>
          <div class="task-name">
            <p>{{ todo.label }}</p>
          </div>
          <button class="closingBtn" @click="removeTodo">
            <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18">
              <path
                fill="#494C6B"
                fill-rule="evenodd"
                d="M16.97 0l.708.707L9.546 8.84l8.132 8.132-.707.707-8.132-8.132-8.132 8.132L0 16.97l8.132-8.132L0 .707.707 0 8.84 8.132 16.971 0z"
              />
            </svg>
          </button>
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
  cursor: pointer;
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
  justify-content: space-between;
  cursor: pointer;
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

.closingBtn {
  border: none;
  cursor: pointer;
}
</style>
