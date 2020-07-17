<template>
  <div id="app">
    <Header />
    <AddTodo @add-todo="addTodo" />
    <Todos v-bind:todos="todos" @del-todo="deleteTodo" />
  </div>
</template>

<script>
import Header from "./components/layout/Header";
import AddTodo from "./components/AddTodo";
import Todos from "./components/Todos";
export default {
  name: "App",
  components: {
    Header,
    AddTodo,
    Todos
  },
  data() {
    return {
      todos: []
    };
  },
  methods: {
    deleteTodo(id) {
      this.todos = this.todos.filter(todo => {
        return todo.id !== id;
      });
    },
    addTodo(newTodo) {
      this.todos = [...this.todos, newTodo];
    }
  },
  created() {
    fetch("https://jsonplaceholder.typicode.com/todos/?_limit=7")
      .then(response => response.json())
      .then(json => (this.todos = json));
  }
};
</script>

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  padding: 0;
  background-color: #a3bffa;
}

h1,
h2,
h3,
h4,
h5,
h6,
p,
a,
span,
li {
  padding: 0;
  margin: 0;
}

input[type="submit"],
.btn {
  cursor: pointer;
  border: 0;
  padding: 0.25rem 0.5rem;
  border-radius: 6px;
}

.visually-hidden {
  position: absolute !important;
  opacity: 0;
  height: 1px;
  width: 1px;
  overflow: hidden;
  clip: rect(1px 1px 1px 1px); /* IE6, IE7 */
  clip: rect(1px, 1px, 1px, 1px);
  white-space: nowrap; /* added line */
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin: 20px auto;
  width: 100%;
  max-width: 480px;
}

.icon {
  height: 18px;
  width: 18px;
}
</style>
