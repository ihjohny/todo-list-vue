<template>
  <div>
    <div v-bind:key="todo.id" v-for="todo in todosList">
      <TodoItem v-bind:todoItem="todo" v-on:del-todo="$emit('del-todo', todo.id)"/>
    </div>
  </div>
</template>

<script>
import TodoItem from './TodoItem'

export default {
  name: "Todos",
  components: {
    TodoItem
  },
  props: ["todosList"]
}
</script>

<style scoped>

</style>