<script setup>
import TodoItem from './TodoItem.vue'
defineProps({
  todos: Array,
})
const emit = defineEmits(['toggle-complete', 'remove-todo'])
const handleToggleComplete = (todoId) => {
  emit('toggle-complete', todoId)
}
const handleRemoveTodo = (todoId) => {
  emit('remove-todo', todoId)
}
</script>
<template>
  <div id="todo-list">
    <div>
      <TodoItem
        v-for="todo in todos"
        :key="todo.id"
        :todo="todo"
        @toggle-complete="handleToggleComplete"
        @remove-todo="handleRemoveTodo"
      />
    </div>
  </div>
</template>
<style scoped>
#todo-list {
  background-color: #fff;
  height: auto;
  margin-inline: auto;
  width: 33%;
  margin-top: -100px;
  border-radius: 8px;
  border: 1px solid #8888;
  box-shadow: 5px 10px #888888;
}
</style>
