<script setup>
import TodoItem from './TodoItem.vue'
</script>
<template>
  <div id="todo-list">
    <div>
      <TodoItem />
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
