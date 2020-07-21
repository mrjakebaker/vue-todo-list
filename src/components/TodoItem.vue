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
		<div class="todo-item__info">
			<p class="todo-item__title">{{ todo.title }}</p>
			<span class="todo-item__due-date">{{ todo.due }}</span>
		</div>
		<div class="todo-item__actions" v-if="todo.completed == false">
			<button
				aria-label="edit"
				class="btn btn--action btn--edit"
				@click="$emit('open-modal', todo.id)"
			>
				<svg
					xmlns="http://www.w3.org/2000/svg"
					viewBox="0 0 24 24"
					class="icon icon--edit"
					fill="none"
					stroke="#000"
					stroke-width="2"
					stroke-linecap="round"
					stroke-linejoin="round"
				>
					<path
						d="M20 14.66V20a2 2 0 01-2 2H4a2 2 0 01-2-2V6a2 2 0 012-2h5.34"
					/>
					<path d="M18 2l4 4-10 10H8v-4L18 2z" />
				</svg>
			</button>
			<button
				aria-label="delete"
				class="btn btn--action btn--delete"
				@click="$emit('del-todo', todo.id)"
			>
				<svg
					viewBox="0 0 24 24"
					class="icon icon--delete"
					xmlns="http://www.w3.org/2000/svg"
					fill="none"
					stroke-width="2"
					stroke-linecap="round"
					stroke-linejoin="round"
				>
					<path
						d="M3 6h18M19 6v14a2 2 0 01-2 2H7a2 2 0 01-2-2V6m3 0V4a2 2 0 012-2h4a2 2 0 012 2v2M10 11v6M14 11v6"
					/>
				</svg>
			</button>
		</div>
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
	background: var(--surface);
	padding: 0.75rem;
	margin-bottom: 0.25rem;
	/* border-bottom: 1px solid #ccc; */
	display: flex;
	flex-wrap: wrap;
	align-items: center;
	border-radius: 6px;
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
	/* box-shadow: 0 1px 2px rgba(0, 0, 0, 0.05),
		inset 0px -15px 10px -12px rgba(0, 0, 0, 0.05); */
	padding: 10px;
	display: inline-block;
	position: relative;
	vertical-align: middle;
	cursor: pointer;
	margin-right: 5px;
}

@media screen and (min-width: 768px) {
	.todo-item__label:hover:before {
		background: var(--success-active);
	}
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

@media screen and (min-width: 768px) {
	.todo-item.is--complete .todo-item__label:hover:before {
		background: var(--warning);
	}
}

@media screen and (min-width: 768px) {
	.todo-item.is--complete .todo-item__label:hover:after {
		/* border-color: #666; */
		border: 0;
	}
}

.todo-item__info {
	padding: 0 0.5rem;
	color: var(--text-on-surface);
}

.todo-item__title {
	color: var(--text-on-surface);
	font-weight: bold;
}

.todo-item__due-date {
	text-transform: uppercase;
	display: inline-block;
	font-size: 0.75rem;
	margin-left: auto;

	margin-top: 0.5rem;
}

.todo-item__actions {
	display: flex;
	margin-left: auto;
	justify-content: space-between;
}

.btn--action {
	background: transparent;
	border-radius: 12px;
	display: flex;
	align-items: center;
	padding: 4px;
}

.btn--edit:hover {
	background: var(--success-active);
}

.btn--edit:hover .icon {
	stroke: #fff;
}

.btn--delete:hover {
	background: var(--error);
}

.btn--delete:hover .icon--delete {
	stroke: #fff;
}

.todo-item__actions .btn--action {
	margin-left: 0.25rem;
	/* margin-right: 0.5rem; */
}

.icon {
	height: 18px;
	width: 18px;
	stroke: var(--text-on-surface);
}

@media screen and (min-width: 768px) {
	.todo-item {
		min-height: 50px;
	}

	.todo-item__title {
		max-width: 350px;
	}

	.todo-item__actions {
		display: none;
	}

	.todo-item:hover .todo-item__actions {
		display: inherit;
	}
}
</style>
