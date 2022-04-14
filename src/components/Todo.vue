<template>
  <div class="flex justify-between item-center py-2 px-2"
       :class="{'bg-green-800': this.todo.done, 'bg-red-800': !this.todo.done}">
    <h1 class="cursor-pointer" @click="toogleTodo">{{ todoporop.todo }}</h1>
    <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" @click="removeTodo">Todo löschen</button>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: ["todoporop", "todoindex"],
  data() {
    return {
      todo: this.todoporop,
    }
  },
  methods: {
    toogleTodo() {
      this.$emit("toggleDone-index", this.todoindex)
    },
    removeTodo() {
      this.$emit("removeTodo-index", this.todoindex)
    }
  }
}
</script>
