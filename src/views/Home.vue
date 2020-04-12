<template>
  <div id="app">
    <!-- components are embeded just like a HTML tag -->
    <!-- v-bind for binding the data as props -->
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import Todos from '../components/Todos';
import AddTodo from '../components/AddTodo';
import axios from 'axios';

export default {
  name: "Home",
  components: {
    // here we define the components that we are going to use
    Todos,
    AddTodo
  },
  data() {
    return {
      todos: []
    }
  },
    methods: {
      deleteTodo(id) {
        // using axios, we use backticks `` for putting the variable
        axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        .then(res => this.todos = this.todos.filter(todo => todo.id !== id))
        .catch(err => console.log(err));

        // .filter is an array function that iterates over it and returns the items
        // that fullfill the condition
        // this.todos = this.todos.filter(
        //   todo => todo.id !== id
        // );
      },
      addTodo(newTodo) {
        // pulling the title and completed from newTodo
        const {title, completed} = newTodo;
        // using axios
        axios.post('https://jsonplaceholder.typicode.com/todos', {
          title,
          completed
        })
        .then(res => this.todos = [...this.todos, res.data])
        .catch(err => console.log(err));

        // with spread operator we copy all the items, and add the new one
        // this.todos = [...this.todos, newTodo];
      },
      
  },
  // fires off when the component loads
  created() {
    console.log(123)
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
    .then(res => this.todos = res.data)
    .catch(err => console.log(err));
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
    background: rgb(35, 145, 68);
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
  }
  .btn:hover {
    background: #666;
  }
</style>
