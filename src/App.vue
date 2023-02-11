<template>
  <div id="app">
    <TodoList />
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue'

export default {
  name: 'app',
  components: {
    TodoList
  }
}
</script>

<style>
#app {
  background-color: #A8E6CF;
  padding: 0;
  margin: 0;
  height: 100vh;
  width: 100%;
  display: flex;
  justify-content: center;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;

}
</style>
