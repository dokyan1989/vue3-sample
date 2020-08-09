<template>
  <p>Todo App</p>
  <todo-list v-bind:todos="todos"></todo-list>
  <button v-on:click="add()">Add</button>
</template>

<script>
import TodoList from './TodoList.vue'

export default {
  name: 'TodoApp',
  components: {
    TodoList,
  },
  data() {
    return {
      todos: [
        {
          id: 1,
          title: 'Do the dishes',
        },
        {
          id: 2,
          title: 'Take out the trash',
        },
        {
          id: 3,
          title: 'Mow the lawn',
        },
      ],
    }
  },
  methods: {
    add() {
      const id = this.todos.length + 1
      this.todos.push({
        id,
        title: 'do something',
      })
    },
  },
}
</script>

<style>
</style>