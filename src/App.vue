<script>
import Header from './components/Header.vue';
import TodoInput from './components/TodoInput.vue';
import TodoDisplay from './components/TodoDisplay.vue';

export default {
  data() {
    return {
      todos: [
        {
          id: 1,
          text: 'Complete online JavaScript course',
          isChecked: true
        },
        {
          id: 1,
          text: 'Jog around the park 3x',
          isChecked: false
        },
        {
          id: 1,
          text: '10 minutes meditation',
          isChecked: false
        },
        {
          id: 1,
          text: 'Read for 1 hour',
          isChecked: false
        },
        {
          id: 1,
          text: 'Pick up groceries',
          isChecked: false
        },
        {
          id: 1,
          text: 'Complete Todo App on Frontend Mentor',
          isChecked: false
        },
      ],
      filter: 'all',
      isLightTheme: false
    }
  },
  computed: {
    todosFiltered() {
      if (this.filter == 'active') {
        const todos = this.todos.filter(todo => !todo.isChecked);
        if (todos.length) {
          return todos;
        }
      } else if (this.filter == 'checked') {
        const todos = this.todos.filter(todo => todo.isChecked);
        if (todos.length) {
          return todos;
        }
      }
      this.setFilter('all');
      return this.todos;
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
    },
    setFilter(filter) {
      this.filter = filter;
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
      :todos="todosFiltered"
      @deleteTodo="deleteTodo"
      @checkTodo="checkTodo"
      @deleteChecked="deleteChecked"
      :filter="filter"
      @setFilter="setFilter"
    ></TodoDisplay>

  </main>


</template>

<style lang="scss" scoped>
@import './main.scss';


</style>