<template>
  <form @submit.prevent="submit" id="todo-form">
    <label id="priority">
      Priority
      <input
          type="number"
          min="1"
          max="10"
          placeholder="1-10"
          v-model.number="todo.priority"
      />
    </label>

    <label id="title">
      Title
      <input
          type="text"
          placeholder="Get milk..."
          v-model.trim="todo.title"
      />
    </label>

    <button type="submit">➕ </button>
  </form>
</template>

<script>
export default {
  name: 'TodoForm',
  data() {
    return {
      todo: {
        title: '',
        priority: null,
      },
    };
  },
  methods: {
    clearForm() {
      this.todo = {
        title: '',
        priority: null,
      };
    },
    submit() {
      if (
          this.todo.title !== '' &&
          this.todo.priority !== null &&
          this.todo.priority >= 1 &&
          this.todo.priority <= 10
      ) {
        this.$emit('submit', this.todo);
        this.clearForm();
      }
    },
  },
};
</script>

<style scoped>
#todo-form {
  display: flex;
  background-color: #b4c3f2;
  padding: 24px;
  justify-content: center;
  border-radius: 25px;
}

label {
  margin-right: 16px;
  font-size: 1.2rem;
  color: #0d1c4b;
  font-weight: bold;
}

input {
  display: block;
  margin: 8px 0;
  padding: 12px; /* Increased padding for better spacing */
  border-radius: 5px; /* Adjusted border radius */
  border: 1px solid rgba(0, 0, 0, 0.15);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); /* Added subtle shadow */
  transition: border-color 0.2s ease, box-shadow 0.2s ease;
}

input:focus {
  border: 1px solid #42b983;
  outline: 0;
}

button {
  background: none;
  outline: none;
  border: none;
  padding: 0;
  background-color: #42b983;
  margin-left: 8px;
  margin-bottom: 8px;
  border-radius: 50%;
  width: 40px; /* Increased button size */
  height: 40px;
  color: white;
  font-size: 1.2em;
  font-weight: bold;
  align-self: flex-end;
  cursor: pointer;
  transition: background-color 0.2s ease, transform 0.2s ease;
}

button:hover {
  background-color: #379a6f;
  transform: scale(1.1);
}
</style>
