<template>
  <div class="wrapper">
    <div class="container">
      <Header
        @toggle-add-form="toggleAddForm"
        title="Todo"
        :showAddForm="showAddTodo"
      />
      <div v-show="showAddTodo">
        <AddTodo @add-todo="addTodo" />
      </div>
      <TodoList
        @toggle-reminder="toggleReminder"
        @delete-todo="deleteTodo"
        :todos="todos"
        :overflow="showAddTodo"
      />
    </div>
  </div>
</template>

<script>
import Header from "./components/Header";
import AddTodo from "./components/AddTodo";
import TodoList from "./components/TodoList";

export default {
  name: "App",
  components: {
    Header,
    AddTodo,
    TodoList,
  },
  data() {
    return {
      todos: [],
      showAddTodo: false,
    };
  },
  methods: {
    toggleAddForm() {
      this.showAddTodo = !this.showAddTodo;
    },
    async addTodo(todo) {
      const response = await fetch(`http://localhost:3000/todos/`, {
        method: "POST",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(todo),
      }).then((res) => res.json());

      this.todos = await this.fetchTodos();
      return response;
    },
    async fetchTodos() {
      const data = await fetch("http://localhost:3000/todos").then((res) =>
        res.json()
      );

      return data;
    },
    async fetchTodo(id) {
      const data = await fetch(
        `http://localhost:3000/todos/${id}`
      ).then((res) => res.json());

      return data;
    },
    async updateTodo(newData) {
      const response = await fetch(
        `http://localhost:3000/todos/${newData.id}`,
        {
          method: "PUT",
          headers: {
            "Content-type": "application/json",
          },
          body: JSON.stringify(newData),
        }
      ).then((res) => res.json());

      return response;
    },
    async toggleReminder(id) {
      const data = await this.fetchTodo(id);
      const newData = { ...data, reminder: !data.reminder };
      const updatedData = await this.updateTodo(newData);

      this.todos = await this.fetchTodos();
      return updatedData;
    },
    async deleteTodo(id) {
      if (confirm("Are you sure to delete this todo?")) {
        const deletedData = await fetch(`http://localhost:3000/todos/${id}`, {
          method: "DELETE",
        }).then((res) => res.json());

        this.todos = await this.fetchTodos();
        return deletedData;
      }
      return;
    },
  },
  async created() {
    this.todos = await this.fetchTodos();
  },
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: "Nunito", sans-serif;
  color: #333;
}
</style>

<style scoped>
.wrapper {
  background-color: #efefef;
  min-height: 100vh;
  min-width: 100vw;
  display: flex;
  align-items: center;
  justify-content: center;
}

.container {
  background-color: white;
  border-top: 2px solid #dadada;
  border-radius: 8px;
  box-shadow: 0px 6px 20px rgba(0, 0, 0, 0.1);
  padding: 1.5rem;
  margin: 1rem;
  display: flex;
  flex-direction: column;
  width: 400px;
}
</style>
