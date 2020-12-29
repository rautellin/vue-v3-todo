<template>
  <AddTodo v-on:add-todo="addTodo" />
  <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
</template>

<script>
import Todos from "../components/Todos";
import AddTodo from "../components/AddTodo";
export default {
  name: "Home",
  components: { Todos, AddTodo },
  data() {
    return {
      todos: [],
    };
  },
  methods: {
    deleteTodo(id) {
      fetch(`https://jsonplaceholder.typicode.com/todos/${id}`, {
        method: "DELETE",
      })
        .then(() => (this.todos = this.todos.filter((todo) => todo.id !== id)))
        .catch((err) => console.log(err));
    },
    addTodo(newTodo) {
      const { title, completed } = newTodo;

      fetch("https://jsonplaceholder.typicode.com/todos", {
        method: "POST",
        body: JSON.stringify({ title, completed }),
        headers: { "Content-Type": "application/json" },
      })
        .then((res) => res.json())
        .then((json) => (this.todos = [...this.todos, json]))
        .catch((err) => console.log(err));
    },
  },
  created() {
    fetch("https://jsonplaceholder.typicode.com/todos?_limit=10")
      .then((res) => res.json())
      .then((json) => (this.todos = json))
      .catch((err) => console.log(err));
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

ul {
  list-style: none;
  padding: 0;
}
</style>
