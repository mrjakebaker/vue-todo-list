<template>
  <div class="modal">
    <div class="modal-container">
      <div class="modal-header">
        <button class="btn btn--close modal-close" @click="$emit('close')">
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
        <div class="todo-info__title">
          <label for>
            <span>Name</span>
            <input type="text" class="todo-info__title-input" v-model="edittingTodo[0].title" />
          </label>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Modal",
  props: ["todos", "activeModal"],
  computed: {
    edittingTodo() {
      let edittingTodo = this.todos.filter(todo => {
        return todo.id === this.activeModal;
      });

      return edittingTodo;
    }
  }
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
  overflow: auto;
  background-color: rgba(0, 0, 0, 0.8);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

.modal-container {
  width: 300px;
  margin: 0px auto;
  padding: 1rem;
  background-color: #fff;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
  font-family: Helvetica, Arial, sans-serif;
}

.modal-header h3 {
  margin-top: 0;
  color: #42b983;
}

.modal-body {
  margin: 20px 0;
}

.modal-default-button {
  float: right;
}

.todo-info__title-input {
  width: 100%;
  border: 0;
  padding: 1rem;
  background: #ebebeb;
  border-radius: 12px;
}

.todo-info__title-input:focus {
  outline: 0;
  box-shadow: 0 0 10px blue;
}
/*
 * The following styles are auto-applied to elements with
 * transition="modal" when their visibility is toggled
 * by Vue.js.
 *
 * You can easily play with the modal transition by editing
 * these styles.
 */

.modal-enter {
  opacity: 0;
}

.modal-leave-active {
  opacity: 0;
}

.modal-enter .modal-container,
.modal-leave-active .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}
</style>