<template>
  <div class="bg-gray-600 text-white w-1/2 m-auto mt-12">
    <div class="text-center border-b-2 border-black py-4">
      <h1 class="text-3xl py-4">Unsere Todos</h1>
      <p class="text-xl" v-if="openTodos.length > 0">Offene Todos: {{openTodos.length}}</p>
      <p class="text-xl" v-else>Keine Todos</p>
      <div class="mt-4">
        <input type="text" class="shadow appearance-none border rounded py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
        v-model="newTodo">
        <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" @click="addTodo">Add Todo</button>
      </div>
    </div>

    <div v-for="(todo, index) in todos" :key="todo.todo">
      <Todo :todoporop="todo" :todoindex="index" @toggleDone-index="toggleDone" @removeTodo-index="removeTodo"/>
    </div>
  </div>
</template>

<script>
import Todo from './components/Todo.vue'

export default {
  name: 'App',
  data() {
    return {
      newTodo: "",
      todos: [],
    };
  },
  methods: {
    toggleDone(index) {
      this.todos[index].done = !this.todos[index].done
      this.storeTodos()
    },
    removeTodo(index) {
      this.todos.splice(index, 1)
      this.storeTodos()
    },
    addTodo() {
      if(this.newTodo.trim() === "") {
        return
      }
      this.todos.push({todo: this.newTodo, done: false})
      this.storeTodos()
    },
    storeTodos() {
      localStorage.setItem("todos", JSON.stringify(this.todos))
    },
  },
  mounted() {
    let data = localStorage.getItem("todos")
    if(data !== "" && data !== null) {
      this.todos = JSON.parse(data)
    } else {
      this.todos = [];
    }
  },
  computed: {
    openTodos() {
      const openTodos = this.todos.filter((todo) => {
        return !todo.done
      })
      return openTodos
    }
  },
  components: {
    Todo
  }
}
</script>

