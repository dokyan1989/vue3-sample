<template>
  <p class="text">
    You have selected
    <span>{{ count }}</span> seats for a price of $
    <span>{{ total }}</span>
  </p>
</template>

<script>
export default {
  name: 'MovieSelectedResult',
  props: {
    count: Number,
    total: Number,
  },
}
</script>

<style scoped>
p.text {
  margin: 5px 0;
}

p.text span {
  color: #6feaf6;
}
</style>