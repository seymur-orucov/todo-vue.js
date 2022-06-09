<template>
  <div id="app">
    <div class="container">
      <AddTodo />
      <Todos />
    </div>
  </div>
</template>

<script>
import Todos from "./components/Todos.vue";
import AddTodo from "./components/AddTodo.vue";

export default {
  name: "app",
  components: {
    Todos,
    AddTodo,
  },
};
</script>

<style scoped>
body {
  font-family: "Roboto";
  line-height: 116;
  background: #e8f7f0;
}

.container {
  max-width: 1100px;
  margin: auto;
  overflow: auto;
  padding: 02rem;
}
</style>
