<template>
  <div>
    <Header />
    <AddTodo v-on:add-todo="addTodo" />
    <FilterButtons
      v-on:filter-active="filterActive"
      v-on:filter-completed="filterCompleted"
      v-on:filter-reset="filterReset"
    />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import Header from "../components/Header";
import Todos from "../components/Todos";
import AddTodo from "../components/AddTodo";
import FilterButtons from "../components/FilterButtons";
// import axios from 'axios'

export default {
  name: "TodosPage",
  components: {
    Header,
    Todos,
    AddTodo,
    FilterButtons,
  },
  data() {
    return {
      todos: [
        {
          id: 1,
          title: "Shopping",
          completed: false,
        },
        {
          id: 2,
          title: "Gym",
          completed: false,
        },
        {
          id: 3,
          title: "Loundry",
          completed: false,
        },
      ],
      initialTodos: [],
    };
  },
  methods: {
    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
      this.initialTodos = this.todos;
    },
    addTodo(newTodo) {
      this.todos = [...this.todos, newTodo];
      this.initialTodos = this.todos;
    },
    filterActive() {
      this.todos = this.initialTodos;
      this.todos = this.todos.filter((todo) => todo.completed === false);
    },
    filterCompleted() {
      this.todos = this.initialTodos;
      this.todos = this.todos.filter((todo) => todo.completed === true);
    },
    filterReset() {
      this.todos = this.initialTodos;
    },
    mounted() {
      console.log("mounted");
      // this.initialTodos = this.todos;
    },
  },
};
</script>
