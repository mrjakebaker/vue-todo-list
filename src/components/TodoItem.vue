<template>
	<div class="todo-item" :class="{ 'is--complete': todo.completed }">
		<label class="todo-item__label">
			<input
				class="todo-item__checkbox"
				type="checkbox"
				:checked="todo.completed"
				@change="markComplete"
				:id="todo.id"
				title="mark as completed"
			/>
		</label>
		<p class="todo-item__title">
			{{ todo.title }}
		</p>
		<button class="btn btn--delete" @click="$emit('del-todo', todo.id)">
			<svg
				xmlns="http://www.w3.org/2000/svg"
				viewBox="0 0 24 24"
				width="18"
				height="18"
			>
				<path
					class="icon--delete"
					d="M8 6V4c0-1.1.9-2 2-2h4a2 2 0 0 1 2 2v2h5a1 1 0 0 1 0 2h-1v12a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V8H3a1 1 0 1 1 0-2h5zM6 8v12h12V8H6zm8-2V4h-4v2h4zm-4 4a1 1 0 0 1 1 1v6a1 1 0 0 1-2 0v-6a1 1 0 0 1 1-1zm4 0a1 1 0 0 1 1 1v6a1 1 0 0 1-2 0v-6a1 1 0 0 1 1-1z"
				/>
			</svg>
		</button>
	</div>
</template>

<script>
export default {
	name: 'TodoItem',
	props: ['todo'],
	methods: {
		markComplete() {
			this.todo.completed = !this.todo.completed;
		},
	},
};
</script>

<style scoped>
.todo-item {
	background: #5a67d8;
	padding: 0.75rem;
	margin-bottom: 4px;
	/* border-bottom: 1px solid #ccc; */
	display: flex;
	align-items: flex-start;
	border-radius: 6px;
}

.todo-item__title {
	color: #f7fafc;
	padding: 0 0.5rem;
	font-weight: bold;
}

.is--complete {
	opacity: 0.6;
}

.is--complete .todo-item__title {
	text-decoration: line-through;
}

.todo-item__checkbox {
	position: absolute !important;
	height: 1px;
	width: 1px;
	overflow: hidden;
	clip: rect(1px 1px 1px 1px); /* IE6, IE7 */
	clip: rect(1px, 1px, 1px, 1px);
	white-space: nowrap; /* added line */
}

.todo-item__label {
	position: relative;
	cursor: pointer;
}

.todo-item__label:before {
	content: '';
	border-radius: 12px;
	-webkit-appearance: none;
	background-color: transparent;
	border: 2px solid white;
	box-shadow: 0 1px 2px rgba(0, 0, 0, 0.05),
		inset 0px -15px 10px -12px rgba(0, 0, 0, 0.05);
	padding: 10px;
	display: inline-block;
	position: relative;
	vertical-align: middle;
	cursor: pointer;
	margin-right: 5px;
}

.todo-item__label:hover:before {
	background: #48bb78;
}

.todo-item.is--complete .todo-item__label:after {
	content: '';
	display: block;
	position: absolute;
	top: 5px;
	left: 9px;
	width: 4px;
	height: 10px;
	border: solid white;
	border-width: 0 2px 2px 0;
	transform: rotate(45deg);
}

.todo-item.is--complete .todo-item__label:hover:before {
	background: #faf089;
}

.todo-item.is--complete .todo-item__label:hover:after {
	border-color: #666;
}

.btn--delete {
	margin-left: auto;
	background: #fff5f5;
	border-radius: 12px;
	display: flex;
	align-items: center;
	padding: 4px;
}

.btn--delete:hover {
	background: #f56565;
}

.btn--delete:hover .icon--delete {
	fill: #fff;
}

.icon--delete {
	fill: #5a67d8;
}
</style>
