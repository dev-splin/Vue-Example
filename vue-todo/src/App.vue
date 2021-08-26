<template>
  <div id="app">
    <todo-header></todo-header>
    <todo-input v-on:addTodo="addTodo"></todo-input>
    <todo-list v-bind:propsdata="todoItems" v-on:removeTodo="removeTodo"></todo-list>
    <todo-footer v-on:clearTodo="clearTodo"></todo-footer>
  </div>
</template>

<script>
import TodoFooterVue from './components/TodoFooter.vue'
import TodoHeaderVue from './components/TodoHeader.vue'
import TodoInputVue from './components/TodoInput.vue'
import TodoListVue from './components/TodoList.vue'

export default {
  components : {
    'TodoHeader' : TodoHeaderVue,
    'TodoInput' : TodoInputVue,
    'TodoList' : TodoListVue,
    'TodoFooter' : TodoFooterVue
  },
  created() {
    if(localStorage.length > 0) {
      for(let i = 0 ; i < localStorage.length; ++i) {
        this.todoItems.push(localStorage.key(i));
      }
    }
  },
  data() {
    return {
      todoItems: []
    }
  },
  methods: {
    addTodo(todoItem) {
      localStorage.setItem(todoItem, todoItem);
      this.todoItems.push(todoItem);
    },
    clearTodo() {
      localStorage.clear();
      this.todoItems = [];
    },
    removeTodo(todoItem, index) {
      localStorage.removeItem(todoItem);
      this.todoItems.splice(index, 1);
    }
  },
}

</script>

<style>
  body {
    text-align: center;
    background-color: #f6f6f8;
  }
  input {
    border-style: groove;
    width: 200px;
  }
  button {
    border-style: groove;
  }
  .shadow {
    box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
  }
</style>