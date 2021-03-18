<template>
  <button @click="onClick" :class="`${color}`">
    {{ text }}
  </button>
</template>

<script>
export default {
  name: "Button",
  methods: {
    onClick() {
      this.$emit("toggle-add-form");
    },
  },
  props: ["text", "color"],
};
</script>

<style scoped>
.green {
  background-color: green;
}

.green:hover {
  background-color: rgb(0, 92, 0);
}

.red {
  background-color: red;
}

.red:hover {
  background-color: rgb(92, 0, 0);
}

button {
  border: none;
  border-radius: 4px;
  padding: 0.5rem 1rem;
  color: white;
  font-size: 14px;
  font-weight: 600;
  letter-spacing: 0.025rem;
  cursor: pointer;
}

button:focus {
  outline: none;
}
</style>