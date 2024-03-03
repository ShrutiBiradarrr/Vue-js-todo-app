<template>
  <div class="todo-card">
    <h2>{{ title }}</h2>
    <p>{{ description }}</p>
    <button @click="$emit('delete')">Delete</button>
  </div>
</template>

<script>
export default {
  props: {
    title: String,
    description: String
  }
}
</script>

<style scoped>
.todo-card {
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 10px;
  margin-bottom: 10px;
}

.todo-card button {
  margin-top: 10px;
}
</style>
