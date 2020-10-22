<template>
  <div>
    <Header />
    <AddTodo v-on:add-todo="addTodo" />
    <FilterButtons
      v-on:filter-active="filterActive"
      v-on:filter-completed="filterCompleted"
      v-on:filter-reset="filterReset"
    />
    <ProgressBar v-bind:amountCompleted="amountCompleted" />
    <Todos
      v-bind:todos="todos"
      v-on:del-todo="deleteTodo"
      v-on:countCompleted="countCompleted"
    />
  </div>
</template>

<script>
import Header from "../components/Header";
import Todos from "../components/Todos";
import AddTodo from "../components/AddTodo";
import FilterButtons from "../components/FilterButtons";
import ProgressBar from "../components/ProgressBar";

export default {
  name: "TodosPage",
  components: {
    Header,
    Todos,
    AddTodo,
    FilterButtons,
    ProgressBar,
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
      amountCompleted: 0,
    };
  },
  mounted() {
    this.initialTodos = this.todos;
  },
  methods: {
    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
      this.initialTodos = this.todos;
      this.countCompleted();
    },
    addTodo(newTodo) {
      this.todos = [...this.todos, newTodo];
      this.initialTodos = this.todos;
      this.countCompleted();
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
    countCompleted() {
      const amountTodos = this.todos.length;
      let count = 0;
      for (let todo of this.todos) {
        if (todo.completed) count++;
      }
      if (amountTodos) {
        this.amountCompleted = (count / amountTodos) * 100;
      } else {
        this.amountCompleted = 100;
      }
    },
  },
};
</script>
