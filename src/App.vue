<template>
	<div id="app">
		<Header />
		<AddTodo @add-todo="addTodo" />
		<Todos v-bind:todos="todos" @del-todo="deleteTodo" />
	</div>
</template>

<script>
import db from './components/firebaseInit';
import moment from 'moment';
import Header from './components/layout/Header';
import AddTodo from './components/AddTodo';
import Todos from './components/Todos';
export default {
	name: 'App',
	components: {
		Header,
		AddTodo,
		Todos,
	},
	data() {
		return {
			todos: [],
		};
	},
	methods: {
		deleteTodo(id) {
			this.todos = this.todos.filter((todo) => {
				return todo.id !== id;
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

		db.collection('todos')
			.get()
			.then((querySnapshot) => {
				querySnapshot.forEach((doc) => {
					console.log(doc.data().due);
					const data = {
						id: doc.id,
						title: doc.data().title,
						completed: doc.data().completed,
						due: moment(doc.data().due.seconds * 1000, 'x').format(
							'dddd, MMMM Do YYYY'
						), // Monday
					};
					this.todos.push(data);
				});
			});
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

input[type='submit'],
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
</style>
