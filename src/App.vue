<template>
  <div id="app" class="container">
    <h1 class="my-4">Todo App</h1>
    <TodoForm @add-todo="fetchTodoList"/>
    <hr>
    <TodoList
      @todo-change="fetchTodoList"
      :todoList="todoList"
    />
  </div>
</template>

<script>
import axios from 'axios'
import TodoForm from '@/components/TodoForm'
import TodoList from '@/components/TodoList'

export default {
  name: 'App',
  components: {
    TodoForm,
    TodoList,
  },
  data() {
    return {
      todoList: [],
    }
  },
  methods: {
    fetchTodoList() {
      const SERVER_IP = process.env.VUE_APP_SERVER_IP
      axios.get(`${SERVER_IP}/api/v1/todos/`)
        .then(response => {
          this.todoList = response.data
        })
      }
  },
  created() {
    this.fetchTodoList()
  }
}
</script>

<style>
#app {
  text-align: center ;
}
</style>
