<template>
  <div>
    <h3>Todos</h3>
    <div class="legend">
      <span>Double click to mark as complete</span>
      <span> <span class="incomplete-box"></span> = Incomplete </span>
      <span> <span class="complete-box"></span> = Complete </span>
    </div>
    <div class="todos">
      <div
        v-for="todo in allTodos"
        :key="todo.id"
        :class="{ 'is-complete': todo.completed }"
        class="todo"
        @dblclick="dblclick(todo)"
      >
        {{ todo.title }}
        <i
          aria-hidden="true"
          class="fa fa-trash"
          @click="deleteTodo(todo.id)"
        ></i>
      </div>
    </div>
  </div>
</template>

<script>
import { mapActions, mapGetters } from "vuex";

export default {
  name: "Todos",
  methods: {
    ...mapActions(["fetchTodos", "deleteTodo", "updateTodo"]),
    dblclick(todo) {
      const updTodo = {
        id: todo.id,
        title: todo.title,
        completed: !todo.completed,
      };

      this.updateTodo(updTodo);
    },
  },
  computed: mapGetters(["allTodos"]),
  created() {
    this.fetchTodos();
  },
};
</script>

<style scoped>
.todos {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 1rem;
}

.todo {
  border: 1px solid #ccc;
  background: #41b883;
  padding: 1rem;
  border-radius: 5px;
  text-align: center;
  position: relative;
  cursor: pointer;
}

i {
  position: absolute;
  right: 10px;
  bottom: 10px;
  color: #fff;
  transition: 0.2s ease-in-out;
}

i:hover {
  color: #b84141;
}

.legend {
  display: flex;
  justify-content: space-around;
  margin-bottom: 1rem;
}

.complete-box {
  display: inline-block;
  width: 10px;
  height: 10px;
  background: #35495e;
}

.incomplete-box {
  display: inline-block;
  width: 10px;
  height: 10px;
  background: #41b883;
}

.is-complete {
  background: #35495e;
  color: #fff;
}

@media (max-width: 500px) {
  .todos {
    grid-template-columns: 1fr;
  }
}
</style>
