<script setup>
import { computed, ref } from 'vue'
import TodoItem from './TodoItem.vue'

const props = defineProps({
  todos: Array,
  darkMode: Boolean,
})

const emit = defineEmits(['toggle-complete', 'remove-todo', 'clear-completed'])

const filter = ref('all')

const incompleteTodosCount = computed(() => props.todos.filter((todo) => !todo.complete).length)

const filteredTodos = computed(() => {
  if (filter.value == 'active') {
    return props.todos.filter((todo) => !todo.complete)
  } else if (filter.value == 'completed') {
    return props.todos.filter((todo) => todo.complete)
  } else {
    return props.todos
  }
})

const setFilter = (selectedFilter) => {
  filter.value = selectedFilter
}

const clearCompleted = () => {
  emit('clear-completed')
}

const handleToggleComplete = (todoId) => {
  emit('toggle-complete', todoId)
}
const handleRemoveTodo = (todoId) => {
  emit('remove-todo', todoId)
}
</script>
<template>
  <div :class="darkMode ? 'dark' : 'light'" id="todo-list">
    <div>
      <TodoItem
        v-for="todo in filteredTodos"
        :key="todo.id"
        :todo="todo"
        @toggle-complete="handleToggleComplete"
        @remove-todo="handleRemoveTodo"
      />
    </div>
    <div class="routes">
      <div>
        <article>
          <span>{{ incompleteTodosCount }}</span> item(s) left
        </article>
      </div>
      <div class="navigation">
        <span class="nav" :class="{ active: filter == 'all' }" @click="setFilter('all')">All</span>
        <span class="nav" :class="{ active: filter == 'active' }" @click="setFilter('active')"
          >Active</span
        >
        <span class="nav" :class="{ active: filter == 'completed' }" @click="setFilter('completed')"
          >Completed</span
        >
      </div>
      <div>
        <span @click="clearCompleted">Clear Completed</span>
      </div>
    </div>
  </div>
</template>
<style scoped>
.light {
  background-color: #fff;
  color: black;
  border: 1px solid #888;
  box-shadow: 5px 10px #888888;
}

.dark {
  background-color: #25273d;
  color: white;
  border: 1px solid #050505;
  box-shadow: 5px 10px #050505;
}

#todo-list {
  height: auto;
  margin-inline: auto;
  width: 33%;
  margin-top: -100px;
  border-radius: 8px;
}

.routes {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-inline: 22px;
  margin-bottom: 22px;
  margin-top: 22px;
  cursor: pointer;
}

.nav {
  padding: 0 10px 0 10px;
}

span:hover {
  color: rgb(33, 33, 199);
}
</style>
