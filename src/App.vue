<template>
  <h1>Vue 3 Todo</h1>
  <form @submit.prevent="addNewTodo">
    <label>New Todo</label>
    <input v-model="newTodo" name="newTodo" />
    <button>Add Todo</button>
  </form>
  <button @click="markAllDone()">Mark all as Done</button>
  Todos:
  <ol>
    <li
      v-for="(todo, index) in todos"
      :key="index"
      :class="{ done: todo.done }"
    >
      <h3 @click="toggleDone(todo)">{{ todo.content }}</h3>
      <button @click="removeTodo(index)">Remove from list</button>
    </li>
  </ol>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const newTodo = ref("");
    const todos = ref([]);

    function addNewTodo() {
      todos.value.push({
        done: false,
        content: newTodo.value,
      });

      this.newTodo = "";
    }

    function toggleDone(todo) {
      todo.done = !todo.done;
    }

    function removeTodo(todoIndex) {
      todos.value.splice(todoIndex, 1);
    }

    function markAllDone() {
      todos.value.forEach((todo) => (todo.done = true));
    }

    return {
      addNewTodo,
      newTodo,
      todos,
      toggleDone,
      removeTodo,
      markAllDone,
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

ol li {
  cursor: pointer;
  text-align: left;
}

.done {
  text-decoration: line-through;
}
</style>
