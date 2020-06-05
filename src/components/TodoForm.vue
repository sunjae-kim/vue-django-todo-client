<template>
    <form class="input-group mb-3" @submit="onSubmit">
    <input type="text" class="form-control" v-model="content">
    <div class="input-group-append">
      <button class="btn btn-outline-secondary">Add</button>
    </div>
  </form>
</template>

<script>
import axios from 'axios'

export default {
  name: 'TodoForm',
  data() {
    return {
      content: '',
    }
  },
  methods: {
    onSubmit(event) {
      const SERVER_IP = process.env.VUE_APP_SERVER_IP
      event.preventDefault()
      axios
        .post(`${SERVER_IP}/api/v1/todos/`, {
          content: this.content,
        })
        .then(() => {
          this.$emit('add-todo')
        });
      this.content = ''
    },
  },
};
</script>

<style>
  #todoForm {
    width: 100%;
    display: flex;
    justify-content: center;
  }
</style>
