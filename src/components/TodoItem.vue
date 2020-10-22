<template>
  <div
    v-on:change="$emit('countCompleted')"
    class="todo-item"
    v-bind:class="{ 'is-complete': todo.completed }"
  >
    <p>
      <input type="checkbox" v-on:change="markComplete" />
      {{ todo.title }}
      <button class="del" @click="$emit('del-todo', todo.id)">x</button>
    </p>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo"],
  methods: {
    markComplete() {
      this.todo.completed = !this.todo.completed;
      // let data = localStorage.getItem("todos");
      // const todosInStorage = JSON.parse(data);
      // const index = todosInStorage.findIndex((todo) => todo.id === this.props.todo.id);
      // console.log(this.props.todo.id);
      // console.log(index);
      // todosInStorage[index] = !todosInStorage[index].completed;
      // const updatedTodos = [...todosInStorage];
      // localStorage.setItem("todos", JSON.stringify(updatedTodos));
    },
  },
};
</script>

<style scoped>
.todo-item {
  background-color: #f4f4f4;
  padding: 10px;
  border-bottom: 1px #ccc dotted;
}

.is-complete {
  text-decoration: line-through;
}

.del {
  background-color: #ff0000;
  color: #fff;
  border: none;
  padding: 5px 9px;
  border-radius: 50%;
  cursor: pointer;
  float: right;
}
</style>
