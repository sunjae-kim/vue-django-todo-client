<template>
  <section>
    <TodoListItem
      @todo-change="$emit('todo-change')"
      v-for="todo in todoList"
      :key="todo.id"
      :todo="todo"
    />
  </section>
</template>

<script>
import TodoListItem from '@/components/TodoListItem'

export default {
  name: 'TodoList',
  components: {
    TodoListItem,
  },
  props: {
    todoList: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style></style>
