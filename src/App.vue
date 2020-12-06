<template>
  <TodoList/>
</template>

<script>
import TodoList from './components/TodoList.vue'

export default {
  name: 'App',
  components: {
    TodoList
  }
}
</script>

<style>
#app {
  background-color: #1a1e6b;
}
</style>
