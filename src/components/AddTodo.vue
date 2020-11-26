<template>
	<div class="new-todo">
		<form class="new-todo__form">
			<div class="input-group">
				<input
					aria-label="Add new Todo"
					type="text"
					placeholder="Add new Todo..."
					name="title"
					v-model="title"
					class="new-todo__title"
				/>
				<label>
					<input
						@click="addTodo"
						type="submit"
						value
						class="visually-hidden new-todo__submit"
					/>
					<span type="submit" class="btn btn--add" tabindex="-1">
						<svg
							viewBox="0 0 24 24"
							class="icon icon--add"
							xmlns="http://www.w3.org/2000/svg"
							fill="none"
							stroke-width="2"
							stroke-linecap="round"
							stroke-linejoin="round"
						>
							<path d="M12 5v14M5 12h14" />
						</svg>
					</span>
				</label>
			</div>
		</form>
	</div>
</template>

<script>
import { v4 as uuidv4 } from 'uuid';
import * as firebase from 'firebase';
import db from '../components/firebaseInit';
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

			if (this.title !== '') {
				var dueDate = firebase.firestore.Timestamp.fromDate(new Date());
				const newTodo = {
					todo_id: uuidv4(),
					title: this.title,
					completed: false,
					due: dueDate,
				};

				this.$emit('add-todo', newTodo);
				this.title = '';

				db.collection('todos')
					.add(newTodo)
					.then((docRef) => {
						console.log('Todo added: ', docRef.id);
					})
					.catch((error) => {
						console.error('Error adding todo: ', error);
					});
			}
		},
	},
};
</script>

<style>
.new-todo {
	margin-bottom: 1.25rem;
}

.new-todo__form {
	padding: 0.5rem;
	display: flex;
	background: #c3dafe;
	border-radius: 6px;
}

.input-group {
	display: flex;
	width: 100%;
}

.new-todo__title {
	flex: 1;
	padding: 0.5rem;
	margin-right: 0.5rem;
	border: 0;
	border-radius: 6px;
}

.new-todo__submit:focus + .btn {
	/* border: 1px solid red; */
	outline-offset: 0px;
	outline: -webkit-focus-ring-color auto 1px;
}

.btn--add {
	background: #9ae6b4;
	display: flex;
	height: 100%;
	align-items: center;
}

.btn--add:hover {
	background: #48bb78;
	color: white;
}

.icon--add {
	stroke: #234e52;
}
</style>
