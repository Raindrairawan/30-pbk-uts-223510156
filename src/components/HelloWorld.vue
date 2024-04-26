<template>
  <div class="todo-app">
    <h1>My To-Do List</h1>
    <form @submit.prevent="addTodo">
      <input v-model="newTodo" placeholder="Add a new to-do" />
      <button type="submit">Add</button>
    </form>
    <ul>
      <li v-for="(todo, index) in todos" :key="index">
        <input type="checkbox" v-model="todo.completed" @change="toggleCompleted(todo.id)" />
        <span :class="{ completed: todo.completed }">{{ todo.text }}</span>
        <button @click="removeTodo(todo.id)">Cancel</button>
      </li>
    </ul>
    <h2>Incomplete To-Dos:</h2>
    <ul>
      <li v-for="(todo, index) in filteredTodos" :key="index">
        <input type="checkbox" v-model="todo.completed" @change="toggleCompleted(todo.id)" />
        <span :class="{ completed: todo.completed }">{{ todo.text }}</span>
        <button @click="removeTodo(todo.id)">Cancel</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodo: '',
      todos: [
        { id: 1, text: 'Buy groceries', completed: false },
        { id: 2, text: 'Do laundry', completed: false },
        { id: 3, text: 'Walk the dog', completed: true },
      ],
    };
  },
  computed: {
    filteredTodos() {
      return this.todos.filter((todo) => !todo.completed);
    },
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim()) {
        const newId = this.todos.length + 1;
        this.todos.push({ id: newId, text: this.newTodo.trim(), completed: false });
        this.newTodo = '';
      }
    },
    removeTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
    toggleCompleted(id) {
      const todo = this.todos.find((t) => t.id === id);
      if (todo) {
        todo.completed = !todo.completed;
      }
    },
  },
};
</script>

<style scoped>
.todo-app {
  font-family: Arial, sans-serif;
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

ul {
  list-style: none;
  padding: 0;
  margin: 10px0;
}

li {
  display: flex;
  align-items: center;
  margin-bottom: 5px;
}

input[type="checkbox"] {
  margin-right: 10px;
}

.completed {
  text-decoration: line-through;
  color: #ccc;
}
</style>