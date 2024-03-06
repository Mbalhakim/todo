<template>
  <div id="main">
    <h1>Todo App</h1>

    <todo-form @submit="addTodo" />

    <div class="todo-section">
      <h3 v-if="sortedTodos.length > 0">Todo</h3>
      <ul>
        <list-item
            v-for="(todo, i) in sortedTodos"
            :key="i"
            :todo="todo"
            @delete="deleteTodo(i)"
            @complete="completeTodo(i)"
            @edit="completeTodo(i)"
        />
      </ul>
    </div>

    <div class="completed-section">
      <h3 v-if="completed.length > 0">Done</h3>
      <ul>
        <list-item
            v-for="(todo, i) in completed"
            :key="i"
            :todo="todo"
            :isCompleted="true"
            @delete="deleteTodo({ i, isCompleted: true })"
        />
      </ul>
    </div>
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
      completed: [],

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
  font-size: 2.2em;
  margin: 40px 0;
  color: #5c3a21;
}

ul {
  margin: 0;
  padding: 0;
}

#main {
background-color: #f2c4b4 ;
  max-width: 400px;
  border-radius: 30px ;
  margin: 20px auto;
  padding: 16px;
  flex-grow: 1;
  overflow-y: auto;
}

.todo-section,
.completed-section {

  margin-top: 24px;
}

</style>