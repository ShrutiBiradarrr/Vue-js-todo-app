<template>
  <div>
    <h1>Todo List</h1>
    <form @submit.prevent="addTodo">
      <input type="text" v-model="newTodo.title" placeholder="Title">
      <textarea v-model="newTodo.description" placeholder="Description"></textarea>
      <button type="submit">Add Todo</button>
    </form>
    <div class="todo-list">
      <TodoItem v-for="(todo, index) in todos" :key="index" :title="todo.title" :description="todo.description"
        @delete="deleteTodo(index)" />
    </div>
  </div>
</template>

<script>
import TodoItem from './components/TodoItem.vue'

export default {
  components: {
    TodoItem
  },
  data() {
    return {
      todos: [],
      newTodo: {
        title: '',
        description: ''
      }
    };
  },
  methods: {
    addTodo() {
      this.todos.push({ ...this.newTodo });
      this.newTodo.title = '';
      this.newTodo.description = '';
    },
    deleteTodo(index) {
      this.todos.splice(index, 1);
    }
  }
}
</script>

<style scoped>
/* Add your CSS styles here */
</style>
