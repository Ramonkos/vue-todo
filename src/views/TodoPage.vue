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
      v-bind:todos="filteredTodos"
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
      todos: [],
      filteredTodos: [],
      amountCompleted: 0,
    };
  },
  mounted() {
    let data = localStorage.getItem("todos");
    if (data) {
      this.filteredTodos = this.todos = JSON.parse(data);
    }
  },
  methods: {
    deleteTodo(id) {
      const data = localStorage.getItem("todos");
      const todosInStorage = JSON.parse(data);
      const filtered = todosInStorage.filter((todo) => todo.id !== id);
      localStorage.setItem("todos", JSON.stringify(filtered));
      this.todos = filtered;
      this.filteredTodos = filtered;
      this.countCompleted();
    },
    addTodo(newTodo) {
      let data = localStorage.getItem("todos");
      if (data) {
        const todosInStorage = JSON.parse(data);
        const updatedTodos = [...todosInStorage, newTodo];
        localStorage.setItem("todos", JSON.stringify(updatedTodos));
        this.todos = updatedTodos;
        console.log("in da if", this.todos);
        this.filteredTodos = updatedTodos;
      } else {
        localStorage.setItem("todos", JSON.stringify([newTodo]));
        this.todos = [newTodo];
        this.filteredTodos = [newTodo];
        console.log("in da else", this.todos);
      }
      this.countCompleted();
    },
    filterActive() {
      this.filteredTodos = this.todos.filter(
        (todo) => todo.completed === false
      );
    },
    filterCompleted() {
      this.filteredTodos = this.todos.filter((todo) => todo.completed === true);
    },
    filterReset() {
      this.filteredTodos = this.todos;
    },
    countCompleted() {
      const amountTodos = this.todos.length;
      let count = 0;
      console.log("this.todos", this.todos);
      for (let todo of this.todos) {
        if (todo.completed) count++;
      }
      console.log("count", count);
      if (amountTodos) {
        this.amountCompleted = (count / amountTodos) * 100;
      } else {
        this.amountCompleted = 100;
      }
    },
  },
};
</script>
