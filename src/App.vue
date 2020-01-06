/* eslint-disable no-console */
<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>


<script>
const STORAGE_KEY = "todo-storage";

import Header from "./components/layout/Header";
import Todos from "./components/Todos";
import AddTodo from "./components/AddTodo";
// import axios from "axios";

export default {
  name: "app",
  components: {
    Header,
    Todos,
    AddTodo
  },
  data() {
    return {
      todos: []
    };
  },
  methods: {
    deleteTodo(id) {
      // axios
      //   .delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      //   .then((this.todos = this.todos.filter(todo => todo.id !== id)))
      //   // eslint-disable-next-line no-console
      //   .catch(err => console.log(err));
      this.todos = this.todos.filter(todo => todo.id !== id);
      localStorage.setItem(STORAGE_KEY, JSON.stringify(this.todos));
    },
    addTodo(newTodo) {
      // const { title, completed } = newTodo;
      // axios
      //   .post("https://jsonplaceholder.typicode.com/todos", {
      //     title,
      //     completed
      //   })
      //   .then(res => (this.todos = [...this.todos, res.data]))
      //   // eslint-disable-next-line no-console
      //   .catch(err => console.log(err));
      this.todos = [...this.todos, newTodo];
      localStorage.setItem(STORAGE_KEY, JSON.stringify(this.todos));
    },
    created() {
      // axios
      //   .get("https://jsonplaceholder.typicode.com/todos?_limit=5")
      //   .then(res => (this.todos = res.data))
      //   // eslint-disable-next-line no-console
      //   .catch(err => console.log(err));
      if (localStorage.getItem("todos")) {
        this.todos = JSON.parse(localStorage.getItem(STORAGE_KEY) || "[]");
      }
      // this.todos = JSON.parse(localStorage.getItem(STORAGE_KEY) || "[]");
    }
  }
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}

.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}

.btn:hover {
  background: #666;
}
</style>
