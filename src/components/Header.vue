<template>
  <div class="header">
    <h2>{{ title }}</h2>
    <Button
      @toggle-add-form="$emit('toggle-add-form')"
      :text="showAddForm ? 'Close' : 'Add Item'"
      :color="showAddForm ? 'red' : 'green'"
    />
  </div>
</template>

<script>
import Button from "./Button";
export default {
  name: "Header",
  components: {
    Button,
  },
  props: {
    title: String,
    showAddForm: Boolean,
  },
  emits: ["toggle-add-form"],
};
</script>

<style scoped>
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-bottom: 1rem;
  border-bottom: 1px solid #eaeaea;
}

h2 {
  letter-spacing: 0.04rem;
}
</style>