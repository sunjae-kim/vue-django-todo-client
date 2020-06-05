<template>
  <div class="input-group mb-3">
    <div class="input-group-prepend">
      <div class="input-group-text">
        <input type="checkbox" @click="updateTodo" :checked="todo.is_completed">
      </div>
    </div>
    <input type="text" class="form-control" v-model="content">
    <div class="input-group-append">
      <button @click="editTodo" class="btn btn-outline-secondary" type="button">Edit</button>
      <button @click="deleteTodo" class="btn btn-outline-secondary" type="button">&times;</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'TodoListItem',
  data() {
    return {
      content: this.todo.content,
    }
  },
  props: {
    todo: {
      type: Object,
      required: true,
    },
  },
  methods: {
    deleteTodo() {
      const SERVER_IP = process.env.VUE_APP_SERVER_IP;
      axios.delete(`${SERVER_IP}/api/v1/todos/${this.todo.id}/`).then(() => {
        this.$emit('todo-change')
      })
    },
    updateTodo() {
      const SERVER_IP = process.env.VUE_APP_SERVER_IP;
      axios
        .put(`${SERVER_IP}/api/v1/todos/${this.todo.id}/`, {
          ...this.todo,
          is_completed: !this.todo.is_completed,
        })
        .then(() => {
          this.$emit('todo-change')
        })
    },
    editTodo() {
      const SERVER_IP = process.env.VUE_APP_SERVER_IP;
      axios
        .put(`${SERVER_IP}/api/v1/todos/${this.todo.id}/`, {
          ...this.todo,
          content: this.content,
        })
        .then(() => {
          this.$emit('todo-change')
        })
    }
  },
}
</script>

<style></style>
