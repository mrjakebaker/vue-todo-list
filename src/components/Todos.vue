<template>
	<div class="todo__list">
		<transition name="modal">
			<Modal
				v-if="showModal"
				@close="showModal = false"
				:activeModal="activeModal"
				:todos="todos"
			/>
		</transition>
		<div v-if="activeTodo.length > 0" class="todo__list--populated">
			<div v-bind:key="todo.id" v-for="todo in activeTodo">
				<TodoItem
					v-bind:todo="todo"
					@del-todo="$emit('del-todo', todo.id)"
					@open-modal="openModal"
				/>
			</div>
		</div>
		<div class="todo__list--empty" v-else>
			<img src="../assets/complete.svg" height="50" alt="" />
			<h2>
				All Done
			</h2>
		</div>
		<h2 class="todo__list-title">Completed</h2>
		<div v-bind:key="todo.id" v-for="todo in completedTodo">
			<TodoItem v-bind:todo="todo" @del-todo="$emit('del-todo', todo.id)" />
		</div>
	</div>
</template>

<script>
import TodoItem from './TodoItem.vue';
import Modal from './Modal.vue';
export default {
	name: 'Todos',
	components: {
		TodoItem,
		Modal,
	},
	data() {
		return {
			showModal: false,
			activeModal: -1,
		};
	},
	props: ['todos'],
	methods: {
		openModal(id) {
			// console.log(id);
			this.activeModal = id;
			this.showModal = true;
		},
	},
	computed: {
		reverseTodos() {
			return this.todos.slice().reverse();
		},
		activeTodo() {
			let activeTodos = this.todos.filter((todo) => {
				return todo.completed !== true;
			});

			return activeTodos.slice().reverse();
		},
		completedTodo() {
			let completedTodos = this.todos.filter((todo) => {
				return todo.completed == true;
			});

			return completedTodos.slice().reverse();
		},
	},
};
</script>

<style scoped>
.todo__list-title {
	margin: 1.5rem 0 1rem;
	font-size: 16px;
}
</style>
