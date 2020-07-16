<template>
	<div class="new-todo">
		<form class="new-todo__form">
			<input
				type="text"
				placeholder="Add new Todo..."
				name="title"
				v-model="title"
				class="new-todo__title"
			/>
			<input @click="addTodo" type="submit" value="+" class="btn btn--add" />
		</form>
	</div>
</template>

<script>
import { v4 as uuidv4 } from 'uuid';
export default {
	name: 'AddTodo',
	data() {
		return {
			title: '',
		};
	},
	methods: {
		addTodo(e) {
			e.preventDefault();

			const newTodo = {
				id: uuidv4(),
				title: this.title,
				completed: false,
			};

			this.$emit('add-todo', newTodo);
			this.title = '';
		},
	},
};
</script>

<style scoped>
.new-todo {
	margin-bottom: 1.25rem;
}

.new-todo__form {
	padding: 0.5rem;
	display: flex;
	background: #ebf4ff;
}

.new-todo__title {
	flex: 1;
	padding: 0.5rem;
	margin-right: 0.5rem;
	border: 0;
}

.btn--add {
	background: #9ae6b4;
}

.btn--add:hover {
	background: #48bb78;
	color: white;
}
</style>
