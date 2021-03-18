<template>
  <ul :class="[overflow ? 'overflow' : '', 'todo-list']">
    <li :key="todo.id" v-for="todo in todos">
      <Todo
        @toggle-reminder="$emit('toggle-reminder', todo.id)"
        @delete-todo="$emit('delete-todo', todo.id)"
        :todo="todo"
      />
    </li>
  </ul>
</template>

<script scoped>
import Todo from "./Todo";

export default {
  name: "TodoList",
  components: {
    Todo,
  },
  props: {
    todos: Object,
    overflow: Boolean,
  },
  emits: ["toggle-reminder", "delete-todo"],
};
</script>

<style scoped>
.todo-list {
  list-style: none;
  display: flex;
  flex-direction: column;
  row-gap: 0.5rem;
  padding-top: 1rem;
}

.todo-list.overflow {
  max-height: 15rem;
  overflow: auto;
}
</style>