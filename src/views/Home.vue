<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todosList="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import AddTodo from "../components/AddTodo";
import Todos from '../components/Todos';
import axios from 'axios';

export default {
  name: 'Home',
  components: {
    AddTodo,
    Todos
  },
  data() {
    return {
      todos: []
    }
  },
  methods: {
    deleteTodo: function (id) {
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
          .then(this.todos = this.todos.filter(todo => todo.id !== id))
          .catch(e => console.log(e));
    },
    addTodo(newTodo) {
      const {title, completed} = newTodo;
      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title,
        completed
      }).then(res => this.todos = [...this.todos, res.data])
          .catch(e => console.log(e));
    }
  },
  created() {
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=10')
        .then(res => this.todos = res.data)
        .catch(e => console.log(e));
  }
}
</script>

<style>
* {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
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
