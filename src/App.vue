<template>
  <div class="m-12 ">
    <div class="bg-gradient-to-r from-fuchsia-600 to-purple-600 p-12  w-[60%]  mx-auto text-center rounded-lg">
      <h1 class="text-4xl font-bold text-white m-8 ">Todo App</h1>
      <form @submit.prevent="addTodo">
        <div>
          <input type="text" v-model="newTodo.title" placeholder="Title" required
            class="p-6 m-4 w-[60%] bg-white rounded-full   shadow-inner focus:outline-none focus:ring-4 focus:ring-purple-400 focus:border-transparent glow">
        </div>
        <div>
          <textarea v-model="newTodo.description" placeholder="Description" required
            class="p-4  w-[60%]  bg-white rounded-full  shadow-inner focus:outline-none focus:ring-4 focus:ring-purple-400 focus:border-transparent glow"></textarea>
        </div>

        <div class="flex justify-center items-center my-12 ">
          <button type="submit"
            class="bg-green-500 hover:bg-green-600 text-white p-4 mr-4 w-[20%] text-lg font-semibold rounded-full">Add
            Todo</button>
          <button type="button" @click="clearAllTodos"
            class="bg-red-500 hover:bg-red-500 text-white p-4 w-[20%] font-semibold text-lg rounded-full">Clear
            All</button>
        </div>

      </form>
    </div>


    <div class="flex flex-wrap justify-center ">

      <TodoItem v-for="(todo, index) in todos" :key="index" :title="todo.title" :description="todo.description"
        :color="todo.color" @delete="deleteTodo(index)" />
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
        description: '',
        color: ''
      },
      colors: ['bg-gradient-to-tr from-blue-800 via-violet-600 to-indigo-900', 'bg-gradient-to-r from-pink-500 to-rose-500', 'bg-gradient-to-r from-fuchsia-500 to-cyan-500', 'bg-gradient-to-r from-amber-500 to-pink-500', 'bg-gradient-to-r from-indigo-400 to-cyan-400', 'bg-gradient-to-r from-amber-300 to-rose-400']
    };
  },
  created() {
    // Retrieve todos from local storage when component is created
    const storedTodos = localStorage.getItem('todos');
    if (storedTodos) {
      this.todos = JSON.parse(storedTodos);
    }
  },
  watch: {
    // Watch for changes in todos and save to local storage
    todos: {
      handler(newTodos) {
        localStorage.setItem('todos', JSON.stringify(newTodos));
      },
      deep: true
    }
  },
  methods: {
    addTodo() {
      const randomIndex = Math.floor(Math.random() * this.colors.length);
      this.newTodo.color = this.colors[randomIndex];
      this.todos.push({ ...this.newTodo });
      this.newTodo.title = '';
      this.newTodo.description = '';
      console.log("todo added successfully")
    },
    deleteTodo(index) {
      this.todos.splice(index, 1);
      console.log("todo deleted successfully with index :", index);
    },
    clearAllTodos() {
      this.todos = [];
      console.log("all todos get cleared successfully")
    }
  }
}
</script>
