<template>
  <div id="app">
    <Header />
    <AddTodo @add-todo="addTodo" />
    <div v-if="todos.length == 0" class="loading">Loading</div>
    <Todos :todos="todos" :isLoading="isLoading" @del-todo="deleteTodo" v-else />
  </div>
</template>

<script>
import db from "./components/firebaseInit";
import moment from "moment";
import Header from "./components/layout/Header";
import AddTodo from "./components/AddTodo";
import Todos from "./components/Todos";
export default {
  name: "App",
  components: {
    Header,
    AddTodo,
    Todos,
  },
  data() {
    return {
      todos: [],
      isLoading: true,
    };
  },
  methods: {
    deleteTodo(id) {
      console.log(id);
      db.collection("todos")
        .where("todo_id", "==", id)
        .get()
        .then((querySnapshot) => {
          querySnapshot.forEach((doc) => {
            doc.ref
              .delete()
              .then(() => {
                console.log("Document successfully deleted!");
              })
              .catch(function (error) {
                console.error("Error removing document: ", error);
              });
          });
        });
      this.todos = this.todos.filter((todo) => {
        return todo.todo_id !== id;
      });
    },
    addTodo(newTodo) {
      this.todos = [...this.todos, newTodo];
    },
  },
  created() {
    // fetch('https://jsonplaceholder.typicode.com/todos/?_limit=7')
    // 	.then((response) => response.json())
    // 	.then((json) => (this.todos = json))
    console.log(this.isLoading);
    db.collection("todos")
      .get()
      .then((querySnapshot) => {
        querySnapshot.forEach((doc) => {
          const data = {
            id: doc.id,
            todo_id: doc.data().todo_id,
            title: doc.data().title,
            completed: doc.data().completed,
            due: moment(doc.data().due.seconds * 1000, "x").format(
              "dddd, MMMM Do YYYY"
            ),
          };
          this.todos.push(data);
        });
      })
      .then((this.isLoading = false));
    console.log(this.isLoading);
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}

:root {
  --background: #a3bffb;
  --surface: #5a67d8;

  --primary: #5a67d8;
  --primary-alt: ;
  --secondary: ;
  --secondary-alt: ;

  --text: #3c366b;
  --text-alt: #2c3e50;
  --text-on-surface: #f7fafc;

  --error: #f56565;
  --error-active: ;

  --warning: #faf089;
  --info: ;
  --success: #9ae6b4;
  --success-active: #48bb78;
}

body {
  margin: 0;
  padding: 0;
  background-color: var(--background);
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

.btn--right {
  margin-left: auto;
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
  color: var(--text);
  margin: 20px auto;
  width: 100%;
  max-width: 480px;
  padding: 0 0.5rem;
}

.icon {
  height: 18px;
  width: 18px;
}

input[type="color"],
input[type="date"],
input[type="datetime"],
input[type="datetime-local"],
input[type="email"],
input[type="month"],
input[type="number"],
input[type="password"],
input[type="search"],
input[type="tel"],
input[type="text"],
input[type="time"],
input[type="url"],
input[type="week"],
select:focus,
textarea {
  font-size: 16px;
}

.loading {
  text-align: center;
}
</style>
