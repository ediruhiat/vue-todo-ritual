<template>
  <div
    @dblclick="$emit('toggle-reminder', todo.id)"
    :class="[todo.reminder ? 'reminder' : '', 'todo']"
  >
    <p>{{ todo.message }}</p>
    <small>{{ todo.date }}</small>
    <div @click="$emit('delete-todo', todo.id)" class="delete">x</div>
  </div>
</template>

<script>
export default {
  name: "Todo",
  props: ["todo"],
};
</script>

<style scoped>
.todo {
  position: relative;
  display: flex;
  flex-direction: column;
  row-gap: 0.5rem;
  padding: 0.5rem;
  background-color: #e9e9e9;
  border: 1px solid #d9d9d9;
  border-radius: 5px;
  letter-spacing: 0.03rem;
}

.todo.reminder {
  border-left: 3px solid royalblue;
}

.delete {
  position: absolute;
  right: 0.5rem;
  top: 50%;
  transform: translateY(-50%);
  font-weight: 600;
  color: red;
  cursor: pointer;
}

small {
  color: #aeaeae;
  font-weight: 600;
}
</style>