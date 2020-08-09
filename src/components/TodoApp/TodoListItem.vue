<template>
  <li>{{ todo.id }} - {{ todo.title }}</li>
</template>

<script>
export default {
  name: 'TodoItem',
  props: {
    todo: Object,
  },
}
</script>

<style sc>
</style>