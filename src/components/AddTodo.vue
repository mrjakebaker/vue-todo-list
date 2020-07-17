<template>
  <div class="new-todo">
    <form class="new-todo__form">
      <div class="input-group">
        <input
          type="text"
          placeholder="Add new Todo..."
          name="title"
          v-model="title"
          class="new-todo__title"
        />
        <label>
          <input @click="addTodo" type="submit" value class="visually-hidden" />
          <button class="btn btn--add">
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
          </button>
        </label>
      </div>
    </form>
  </div>
</template>

<script>
import { v4 as uuidv4 } from "uuid";
export default {
  name: "AddTodo",
  data() {
    return {
      title: ""
    };
  },
  methods: {
    addTodo(e) {
      e.preventDefault();

      const newTodo = {
        id: uuidv4(),
        title: this.title,
        completed: false
      };

      this.$emit("add-todo", newTodo);
      this.title = "";
    }
  }
};
</script>

<style scoped>
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
