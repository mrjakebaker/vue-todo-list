<template>
	<div class="todo__list">
		<div v-bind:key="todo.id" v-for="todo in reverseTodos">
			<TodoItem v-bind:todo="todo" @del-todo="$emit('del-todo', todo.id)" />
		</div>
	</div>
</template>

<script>
import TodoItem from './TodoItem.vue';
export default {
	name: 'Todos',
	components: {
		TodoItem,
	},
	props: ['todos'],

	computed: {
		reverseTodos() {
			return this.todos.slice().reverse();
		},
	},
};
</script>

<style scoped></style>
