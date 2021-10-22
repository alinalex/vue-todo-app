<template>
  <h2>Todo App</h2>
  <form @submit.prevent="addTodo">
    <label>Your new todo</label>
    <input name="todo" v-model="todo" />
    <button>Add todo</button>
  </form>

  <ul>
    <li v-for="(todo, index) in todos" :key="index">
      <span @click="markTodoAsDone(todo)" :class="{ done: todo.done }">
        {{ todo.content }}
      </span>
      <button @click="removeTodo(index)">remove</button>
    </li>
  </ul>
</template>

<script>
import { ref } from 'vue';

export default {
  name: 'App',
  setup() {
    const todo = ref('');
    const todos = ref([]);

    function addTodo() {
      if (todo.value) {
        todos.value.push({
          content: todo.value,
          done: false,
        });

        todo.value = '';
      }
    }

    function markTodoAsDone(todo) {
      todo.done = !todo.done;
    }

    function removeTodo(index) {
      todos.value.splice(index, 1);
    }

    return {
      todo,
      todos,
      addTodo,
      markTodoAsDone,
      removeTodo,
    };
  },
};
</script>

<style>
body {
  margin: 0;
  padding: 0;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background-color: #27292d;
  color: white;
}

#app {
  max-width: 600px;
  margin-left: auto;
  margin-right: auto;
  padding: 20px;
}
#app h1 {
  font-weight: bold;
  font-size: 28px;
  text-align: center;
}
#app form {
  display: flex;
  flex-direction: column;
  width: 100%;
}
#app form label {
  font-size: 14px;
  font-weight: bold;
}
#app form input,
#app form button {
  height: 48px;
  box-shadow: none;
  outline: none;
  padding-left: 12px;
  padding-right: 12px;
  border-radius: 6px;
  font-size: 18px;
  margin-top: 6px;
  margin-bottom: 12px;
}
#app form input {
  background-color: transparent;
  border: 2px solid rgba(255, 255, 255, 0.35);
  color: inherit;
}
#app button {
  cursor: pointer;
  background-color: #a0a4d9;
  border: 1px solid #a0a4d9;
  color: #1f2023;
  font-weight: bold;
  outline: none;
  border-radius: 6px;
}
#app h2 {
  font-size: 22px;
  border-bottom: 2px solid rgba(255, 255, 255, 0.35);
  padding-bottom: 6px;
}
#app ul {
  padding: 10px;
}
#app ul li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border: 2px solid rgba(255, 255, 255, 0.35);
  padding: 12px 24px;
  border-radius: 6px;
  margin-bottom: 12px;
}
#app ul li span {
  cursor: pointer;
}
#app ul li .done {
  text-decoration: line-through;
}
#app ul li button {
  font-size: 12px;
  padding: 6px;
}
#app h4 {
  text-align: center;
  opacity: 0.5;
  margin: 0;
}
</style>
