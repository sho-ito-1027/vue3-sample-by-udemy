<script setup lang="ts">
import { provide } from 'vue';
import TodoList from './components/TodoList.vue';
import { todos } from './useTodo';

provide('todos', todos)
// provide('addTodo', addTodo)
</script>

<template>
  <TodoList></TodoList>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
  }
  
  .tab-contents {
    margin-top: 20px;
  }
</style>
