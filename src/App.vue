<script>
import Header from './components/Header.vue';
import TodoInput from './components/TodoInput.vue';
import TodoDisplay from './components/TodoDisplay.vue';

export default {
  data() {
    return {
      todos: [],
      isLightTheme: false
    }
  },
  components: {Header, TodoInput, TodoDisplay},
  methods: {
    toggleTheme() {
      this.isLightTheme = !this.isLightTheme;
      localStorage.setItem('isLightTheme', this.isLightTheme);
    },
    setToLocalStorage() {
      localStorage.setItem('todos', JSON.stringify(this.todos));
    },
    addTodo(todo) {
      this.todos.unshift(todo);
      this.setToLocalStorage();
    },
    deleteTodo(todoId) {
      this.todos = this.todos.filter(todo => todoId != todo.id);
      this.setToLocalStorage();
    },
    deleteChecked() {
      this.todos = this.todos.filter(todo => !todo.isChecked);
      this.setToLocalStorage();
    },
    checkTodo(todoId) {
      this.todos.map((todo) => {
        if (todoId == todo.id) {
          todo.isChecked = !todo.isChecked;
        }
      });
      this.setToLocalStorage();
    }
  },
  mounted() {
    const theme = localStorage.getItem('isLightTheme');
    if (theme == 'true') this.isLightTheme = theme;

    const todos = localStorage.getItem('todos');
    if (todos.length) this.todos = JSON.parse(todos);
  }
}
</script>

<template>

  <main :class="{light: isLightTheme}">

    <Header @toggleTheme="toggleTheme"></Header>

    <TodoInput @addTodo="addTodo"></TodoInput>

    <TodoDisplay
      :todos="todos"
      @deleteTodo="deleteTodo"
      @checkTodo="checkTodo"
      @deleteChecked="deleteChecked"
    ></TodoDisplay>

  </main>


</template>

<style lang="scss" scoped>
@import './main.scss';


</style>