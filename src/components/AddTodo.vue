<template>
  <form @submit="onSubmit" class="add-form">
    <div class="form-control">
      <label for="message">Message</label>
      <input
        type="text"
        v-model="message"
        name="message"
        id="message"
        placeholder="Message..."
      />
    </div>
    <div class="form-control">
      <label for="date">Date</label>
      <input
        type="text"
        v-model="date"
        name="date"
        id="date"
        placeholder="Date..."
      />
    </div>
    <div class="form-control">
      <label for="reminder">Reminder</label>
      <input
        type="checkbox"
        v-model="reminder"
        name="reminder"
        id="reminder"
        placeholder="Reminder..."
      />
    </div>
    <input type="submit" value="Save" class="btn btn-black" />
  </form>
</template>

<script>
export default {
  name: "AddTodo",
  data() {
    return {
      message: "",
      date: "",
      reminder: false,
    };
  },
  methods: {
    onSubmit(e) {
      e.preventDefault();

      if (!this.message) {
        alert("Pleas fill up message!");
        return;
      }

      const newTodo = {
        message: this.message,
        date: this.date,
        reminder: this.reminder,
      };

      this.$emit("add-todo", newTodo);
    },
  },
};
</script>

<style scoped>
.add-form {
  display: flex;
  flex-direction: column;
  row-gap: 0.5rem;
  padding: 1rem 0;
  letter-spacing: 0.03rem;
  border-bottom: 1px solid #eaeaea;
}

.form-control {
  display: flex;
  flex-direction: column;
  row-gap: 0.3rem;
}

.form-control:nth-child(3) {
  position: relative;
  flex-direction: row;
}

input[type="text"] {
  min-height: 2.5rem;
  padding: 0.25rem;
  border-radius: 4px;
  border: 1px solid #9a9a9a;
  font-size: 14px;
}

input[type="text"]:focus {
  outline: none;
  border: 1px solid royalblue;
  box-shadow: 0px 0px 5px rgba(65, 105, 225, 0.1);
}

input[type="checkbox"] {
  position: absolute;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
}

.btn-black {
  background-color: #222;
  border: none;
  border-radius: 4px;
  padding: 0.5rem 1rem;
  color: white;
  font-size: 14px;
  font-weight: 600;
  letter-spacing: 0.025rem;
  cursor: pointer;
}

.btn:hover {
  background-color: rgba(0, 0, 0, 0.8);
}
</style>