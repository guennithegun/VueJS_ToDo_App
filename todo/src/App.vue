<template>
  <div class="centerApp">
    <div class="todoWrapper">
      <div>
        <h1>Road to Succes</h1>
      </div>
      <div>
        <md-field>
          <label>Type here!</label>
          <md-input class="todoInput" v-model="currentTodo" @keydown.enter="addTodo()"></md-input>
          <span class="md-helper-text">Press Enter to add ToDo</span>
        </md-field>
        <ul class="todos">
          <li v-for="todo in todos" :key="todo.id">
            <span v-if="todo.completed === false">
              <input type="checkbox" v-model="todo.completed">
            </span>
            {{ todo.label }}
            <span v-if="todo.completed">DONE</span>
            <button @click="removeTodo(todo)" class="deleteButton"><md-icon>backspace</md-icon></button>
            <span v-model="todo.editedTodoId" @click="editTodo(todo)"><md-icon>create</md-icon></span>
            <span v-if="todo.editedTodoId">
              <input v-model="todo.editedTodo" placeholder="Edit Todo">
              <button @click="updateTodo(todo)">Edit</button>
            </span>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        todos: [],
        currentTodo: '',
        completed: '',
        editedTodoId: '',
        editedTodo: ''
      };
    },
    methods: {
      addTodo() {
        this.todos.push({id: this.todos.length, label: this.currentTodo, completed: false, editedTodoId: false});
        this.currentTodo = '';
      },
      removeTodo(todo) {
        var index = this.todos.indexOf(todo);
        this.todos.splice(index, 1);
      },
      editTodo(todo) {
        todo.editedTodoId = true;
      },
      updateTodo(todo) {
        todo.label = todo.editedTodo;
        todo.editedTodoId = false;
      }
    }
  };
</script>

<style>
  body, html {
    width: 100%;
    height: 100%;
    font-family: 'Roboto', sans-serif;
  }
  html {
    background: url("./assets/stairway.jpg") no-repeat center center fixed;
    -webkit-background-size: cover;
    -moz-background-size: cover;
    -o-background-size: cover;
    background-size: cover;
  }

  li {
    list-style-type: none;
    font-size: 18px;
  }

  h1 {
    text-align: center;
  }

  .todoWrapper {
    width: 100%;
    max-width: 400px;
    min-height: 500px;
    background-color: rgba(65, 66, 136, 0.7);
    padding: 15px;
    border-radius: 4px;
    color: white;
    box-shadow: 0 2px 10px 0 rgba(0, 0, 0, 0.29);
  }

  .centerApp {
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .md-field, .md-input {
    width: 100%;
    height: 30px;
    border-bottom: 2px solid #85CB33;
    background-color: transparent;
    color: white;
    font-size: 18px;
  }

  .md-field label {
    color: #85CB33;
  }

  .deleteButton {
    background-color: transparent;
    border: none;
    cursor: pointer;
    color: white;
  }
</style>
