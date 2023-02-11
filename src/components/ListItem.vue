<template>
<li class="todo-item" :class="{ completed: isCompleted }">
  <p>{{ todo.priority }} | {{ todo.title }}</p>
  <span>
    <button type="button" class ="delete-button" @click="deleteTodo">X</button>

    <button type="button" class ="complete-button" @click="completeTodo" v-if="!isCompleted">✓</button>
  </span>
</li>
</template>

<script>
export default {
  name: 'ListItem',
  props: {
    todo: Object,
    isCompleted: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    deleteTodo() {
      this.$emit('delete')
    },
    completeTodo() {
      this.$emit('complete')
    },

  }
}
</script>

<style scoped>
.todo-item {
  display: flex;
  justify-content: space-between;
  margin: 16px 0;
  padding: 8px;
  padding-left: 16px;
  background-color: #42b983;
  border-radius: 8px;
  color: white;
}

span {
  display: flex;
  align-self: center;
}

button {
  /* clear button styling */
  background: none;
  outline: none;
  border: none;
  padding: 0;

  /* custom styling */
  margin-left: 8px;
  border-radius: 50%;
  width: 32px;
  height: 32px;
  color: white;
}

.delete-button {
  font-weight: bold;
}

.edit-button {
  font-size: 1.2em;
}

.complete-button {
  font-size: 1.2em;
}

button:active {
  background-color: white;
  color: #42b983;
}

.completed {
  background-color: rgba(66, 185, 131, 0.4);
}

.completed > p{
  text-decoration: line-through;
}
</style>
