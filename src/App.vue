<template>
  <div id="app">
    <h1>Todo List</h1>
<div class="app-container">
  <div class="input-container">
    <input type="text" v-model="newTodo" @keyup.enter="addTodo">
    <button class="add-todo-button" @click="addTodo">Add Todo</button>
  </div>
</div>
    <ul>
      <li v-for="(todo, index) in todos" :key="index" :class="{ completed: todo.isCompleted }">
        <div v-if="todo.isEditing">
          <input type="text" v-model="todo.text" @keyup.enter="todo.isEditing = false">
        </div>
        <div v-else>
          {{ todo.text }}
          <button class="edit-button" @click="todo.isEditing = true">Edit</button>
          <button class="complete-button" @click="todo.isCompleted = !todo.isCompleted">
            {{ todo.isCompleted ? 'Uncomplete' : 'Complete' }}
          </button>
          <button class="remove-button" @click="removeTodo(index)">Remove</button>
        </div>
      </li>
    </ul>
    <p>{{ remaining }} todos left</p>
    <button class="clear-button" @click="clearCompleted">Clear completed todos</button>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      newTodo: '',
      todos: []
    }
  },
  computed: {
    remaining() {
      return this.todos.filter(todo => !todo.isCompleted).length;
    }
  },
  methods: {
    addTodo() {
      this.todos.push({ text: this.newTodo, isCompleted: false, isEditing: false });
      this.newTodo = '';
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
    clearCompleted() {
      this.todos = this.todos.filter(todo => !todo.isCompleted);
    }
  }
}
</script>

<style scoped>
.app-container {
  display: flex;
  justify-content: center;
  align-items: center;

}
.input-container {
  display: flex;

}

ul {
  text-decoration: none;
  }

#app {
  text-align: center;
  padding: 10px;
  width: 700px;
  margin: auto;
  background-color: lightgray;
  
}
.clear-button {
  border: solid 2px #f44336;
  padding: 5px 10px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 15px;
  margin: 4px 2px;
  cursor: pointer;
}
.add-todo-button {
  border: solid 2px black;
  height: 40px;
  width: 170px;
  margin: auto;
  font-size: 15px;
}
.edit-button {
  background-color: white;
  border: solid 2px black;
  padding: 4px 10px;
  width: 60px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 15px;
  margin: 4px 2px;
  cursor: pointer;
}
.remove-button {
  background-color: #f44336;
  color: white;
  border: none;
  padding: 5px 10px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 15px;
  margin: 4px 2px;
  cursor: pointer;
}
.complete-button {
  background-color: #008CBA;
  color: white;
  width: 100px;
  border: none;
  padding: 5px 10px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 15px;
  margin: 4px 2px;
  cursor: pointer;
}
.completed {
  text-decoration: line-through;
  color: green;

}
</style>

