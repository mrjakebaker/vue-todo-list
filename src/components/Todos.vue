<template>
  <div class="todo__list">
    <Modal v-if="showModal" @close="showModal = false" :activeModal="activeModal" :todos="todos" />
    <div v-bind:key="todo.id" v-for="todo in activeTodo">
      <TodoItem v-bind:todo="todo" @del-todo="$emit('del-todo', todo.id)" @open-modal="openModal" />
    </div>
    <h2 class="todo__list-title">Completed</h2>
    <div v-bind:key="todo.id" v-for="todo in completedTodo">
      <TodoItem v-bind:todo="todo" @del-todo="$emit('del-todo', todo.id)" />
    </div>
  </div>
</template>

<script>
import TodoItem from "./TodoItem.vue";
import Modal from "./Modal.vue";
export default {
  name: "Todos",
  components: {
    TodoItem,
    Modal
  },
  data() {
    return {
      showModal: false,
      activeModal: -1
    };
  },
  props: ["todos"],
  methods: {
    openModal(id) {
      // console.log(id);
      this.activeModal = id;
      this.showModal = true;
    }
  },
  computed: {
    reverseTodos() {
      return this.todos.slice().reverse();
    },
    activeTodo() {
      let activeTodos = this.todos.filter(todo => {
        return todo.completed !== true;
      });

      return activeTodos.slice().reverse();
    },
    completedTodo() {
      let completedTodos = this.todos.filter(todo => {
        return todo.completed == true;
      });

      return completedTodos.slice().reverse();
    }
  }
};
</script>

<style scoped>
.todo__list-title {
  margin: 1.5rem 0 1rem;
  font-size: 16px;
}
</style>
