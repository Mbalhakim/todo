<template>
  <div id="main">
    <h1>Todo App</h1>
    <todo-form @submit="addTodo" />

    <h3 v-if="sortedTodos.length > 0">Todo</h3>
    <ul>
      <list-item
          v-for="(todo, i) in sortedTodos"
          :key="i"
          :todo="todo"
          @delete="deleteTodo(i)"
          @complete="completeTodo(i)"
          @edit="completeTodo(i)"/>
    </ul>

    <h3 v-if="completed.length > 0">Done</h3>
    <ul>
      <list-item
          v-for="(todo, i) in completed"
          :key="i"
          :todo="todo"
          :isCompleted="true"
          @delete="deleteTodo({ i, isCompleted: true })"/>
    </ul>
  </div>
</template>

<script>
import TodoForm from './TodoForm.vue'
import ListItem from './ListItem.vue'

export default {
  name: 'TodoList',
  components: {
    TodoForm,
    ListItem
  },
  data() {
    return {
      todos: [],
      completed: []
    }
  },
  computed: {
    sortedTodos() {
      let arraytodo = this.todos
      return arraytodo.sort((a, b) => a.priority - b.priority)
    }
  },
  created() {
    // Check if there are todos in local storage, if so, retrieve and set them
    let todosFromLocalStorage = localStorage.getItem("todos");
    if (todosFromLocalStorage) {
      this.todos = JSON.parse(todosFromLocalStorage);
    }
    let completedFromLocalStorage = localStorage.getItem("completed");
    if (completedFromLocalStorage) {
      this.completed = JSON.parse(completedFromLocalStorage);
    }
  },
  methods: {
    addTodo(todo) {
      this.todos.push(todo)
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
    deleteTodo({i, isCompleted}) {
      if (isCompleted) {
        this.completed.splice(i, 1)
        localStorage.setItem("completed", JSON.stringify(this.completed));
      } else {
        this.todos.splice(i, 1)
        localStorage.setItem("todos", JSON.stringify(this.todos));
      }
    },
    completeTodo(index) {
      this.completed.push(this.todos.splice(index, 1)[0])
      localStorage.setItem("todos", JSON.stringify(this.todos));
      localStorage.setItem("completed", JSON.stringify(this.completed));
    },


  }
}

</script>

<style scoped>
h1 {
  text-align: center;
  margin: 40px 0;
  color: #000000;
}

ul {
  margin: 0;
  padding: 0;
}

#main{
  background-color: #FFD3B6;
  border-radius: 20px;
  padding: 20px;
}
</style>