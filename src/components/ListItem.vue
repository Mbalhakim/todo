<template>
  <li class="todo-item" :class="{ completed: isCompleted }" :style="priorityStyle">
    <p>{{ todo.priority }} | {{ todo.title }}</p>
    <span>
      <button
          type="button"
          class="delete-button"
          @click="deleteTodo"
          title="Delete"
      >
        🗑️
      </button>
      <button
          type="button"
          class="complete-button"
          @click="completeTodo"
          v-if="!isCompleted"
          title="Mark as Completed"
      >
        ✓
      </button>
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
      default: false,
    },
  },
  computed: {
    priorityStyle() {
      const priority = this.todo.priority;
      const hue = (priority / 10) * 120; // Map priority to hue (0-120)
      return {
        backgroundColor: `hsl(${hue}, 70%, 50%)`,
      };
    },
  },
  methods: {
    deleteTodo() {
      this.$emit('delete');
    },
    completeTodo() {
      this.$emit('complete');
    },
  },
};
</script>

<style scoped>
.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 16px 0;
  padding: 8px;
  padding-left: 16px;
  border-radius: 8px;
  color: white;
  transition: background-color 0.3s ease;
}

.todo-item:hover {
  background-color: #379a6f;
}

span {
  display: flex;
  align-self: center;
}

button {
  background: none;
  outline: none;
  border: none;
  padding: 0;
  margin-left: 8px;
  border-radius: 50%;
  width: 32px;
  height: 32px;
  color: white;
  cursor: pointer;
  transition: background-color 0.2s ease, transform 0.2s ease;
}

button:hover {
  background-color: white;
  color: #42b983;
  transform: scale(1.1);
}

.completed {
  background-color: rgba(66, 185, 131, 0.4);
  text-decoration: line-through;
}
</style>
