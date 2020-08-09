<template>
  <ul>
    <todo-list-item v-for="todo in todos" v-bind:key="todo.id" v-bind:todo="todo"></todo-list-item>
  </ul>
</template>

<script>
import TodoListItem from './TodoListItem.vue'

export default {
  name: 'TodoList',
  components: {
    TodoListItem,
  },
  props: {
    todos: Array,
  },
}
</script>

<style>
</style>