<template>
  <h1>Todos</h1>
  <ul>
    <li v-for="(item, index) in todos" :key="index">
      <TodoItem v-bind:todo="item" v-on:del-todo="$emit('del-todo', item.id)" />
    </li>
  </ul>
</template>

<script>
import TodoItem from "./TodoItem";

export default {
  name: "Todos",
  emits: ["delTodo"],
  components: { TodoItem },
  props: ["todos"],
};
</script>

<style scoped>
</style>