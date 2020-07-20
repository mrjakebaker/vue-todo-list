<template>
	<div class="modal">
		<div class="modal-wrapper">
			<div class="modal-container">
				<div class="modal-header">
					<button
						class="btn btn--close btn--right modal-close"
						@click="$emit('close')"
					>
						<svg
							xmlns="http://www.w3.org/2000/svg"
							width="24"
							height="24"
							fill="none"
							stroke="#000"
							stroke-width="2"
							stroke-linecap="round"
							stroke-linejoin="round"
						>
							<path d="M18 6L6 18M6 6l12 12" />
						</svg>
					</button>
				</div>
				<div class="modal-body">
					<!-- -->
					<div class="modal-row">
						<div class="edit-item">
							<label class="edit-item__label label-title" for="edit-item-title">
								<span>Name</span>
							</label>
							<input
								id="edit-item-title"
								type="text"
								class="edit-item__input"
								v-model="edittingTodo[0].title"
							/>
						</div>
					</div>
					<!-- -->
					<div class="modal-row">
						2
					</div>
					<!-- -->
					<div class="modal-row">
						3
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: 'Modal',
	props: ['todos', 'activeModal'],
	computed: {
		edittingTodo() {
			let edittingTodo = this.todos.filter((todo) => {
				return todo.id === this.activeModal;
			});

			return edittingTodo;
		},
	},
};
</script>

<style>
.modal {
	position: fixed;
	z-index: 999;
	left: 0;
	top: 0;
	width: 100%;
	height: 100%;
	overflow: hidden;
	background-color: rgba(0, 0, 0, 0.8);
	display: flex;
	justify-content: center;
	align-items: flex-end;
	transition: opacity 0.5s ease;
}

.modal-wrapper {
	width: 100%;
	padding: 1rem 0.5rem 0.25rem;
}

.modal-container {
	min-height: 50vh;
	max-width: 480px;
	width: 100%;
	margin: 0px auto;
	padding: 1rem;
	background-color: var(--surface);
	border-radius: 12px;
	box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
	transition: all 0.3s ease;
	font-family: Helvetica, Arial, sans-serif;
}
.modal-header {
	display: flex;
}

.modal-row {
	margin-bottom: 12px;
}

.edit-item__input {
	width: 100%;
	border: 0;
	padding: 0.75rem;
	background: #ebebeb;
	border-radius: 4px;
	margin-top: 0.25rem;
}

.edit-item__label {
	font-size: 0.875rem !important;
	color: var(--text-on-surface);
	text-transform: uppercase;
	letter-spacing: 0.25em;
}

.edit-item__input:focus {
	outline: 0;
	box-shadow: 0 0 10px var(--error);
}

.modal-enter .modal-container {
	transform: translateY(100px);
	transition: all 2.3s ease;
}

.modal-leave-active {
	opacity: 0;
}

.modal-leave-active .modal-container {
	transform: translateY(100px);
}
</style>
