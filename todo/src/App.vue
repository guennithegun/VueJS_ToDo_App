<template>
  <div class="centerApp">
    <div class="todoWrapper">
      <div>
        <h1>My Road to Succes</h1>
      </div>
      <div>
        <md-field>
          <label>Add ToDo</label>
          <md-input v-model="currentTodo" @keydown.enter="addTodo()"></md-input>
          <span class="md-helper-text">Press Enter to add ToDo</span>
        </md-field>
      </div>
      <hr>
      <div>
        <h2>Steps to Take</h2>
      </div>
      <div>
        <ul class="todos">
          <div class="emptyTodos" v-if="todos.length === 0">
            <h3>The Journey never ends...</h3>
            <p>Add some tasks to ascend the stairs!</p>
          </div>
          <li v-for="todo in todos" :key="todo.id">
            <div>
              <table>
                <tr>
                  <td>
                    <span class="checkCircle" v-if="todo.completed" @click="undoneTodo(todo)"><md-icon>check_circle</md-icon><md-tooltip md-direction="bottom">Uncheck ToDo</md-tooltip></span>
                    <span v-if="todo.completed === false">
                      <input class="checkBox" type="checkbox" v-model="todo.completed">
                      <md-tooltip md-direction="bottom">Check ToDo</md-tooltip>
                    </span>
                  </td>
                  <td>
                    {{ todo.label }}
                  </td>
              </tr>
              </table>
            </div>
            <div class="editToDos">
              <span @click="removeTodo(todo)" class="deleteButton"><md-icon>backspace</md-icon><md-tooltip md-direction="bottom">Delete ToDo</md-tooltip></span>
              <span class="editButton" v-model="todo.editedTodoId" @click="editTodo(todo)"><md-icon>create</md-icon><md-tooltip md-direction="bottom">Edit ToDo</md-tooltip></span>
            </div>
            <div v-if="todo.editedTodoId">
              <md-field>
                <label>Edit ToDo</label>
                <md-input v-model="todo.editedTodo"></md-input>
              </md-field>
              <span class="editDone" @click="updateTodo(todo)"><md-icon>done</md-icon><md-tooltip md-direction="bottom">Apply</md-tooltip></span>
              <span class="abortEdit" v-model="todo.editedTodoId" @click="hideEdit(todo)"><md-icon>clear</md-icon><md-tooltip md-direction="bottom">Cancel</md-tooltip></span>
            </div>
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
      hideEdit(todo) {
        todo.editedTodoId = false;
      },
      updateTodo(todo) {
        todo.label = todo.editedTodo;
        todo.editedTodoId = false;
      },
      undoneTodo(todo) {
        todo.completed = false;
      }
    }
  };
</script>

<style>
  body, html {
    width: 100%;
    height: 100%;
    font-family: 'Roboto', sans-serif;
    padding: 5px;
  }
  html {
    background: url("./assets/stairway.jpg") no-repeat center center fixed;
    -webkit-background-size: cover;
    -moz-background-size: cover;
    -o-background-size: cover;
    background-size: cover;
  }

  ul {
    margin: 30px 0;
    padding: 0;
  }

  li {
    padding: 3px;
    margin: 5px 0;
    list-style-type: none;
    font-size: 18px;
    background-color: rgba(0,0,0, 0.5);
    border-radius: 3px;
    box-shadow: 0 2px 10px 0 rgba(0, 0, 0, 0.29);
  }

  h1, h2 {
    text-align: center;
  }

  h2 {
    position: relative;
    top: 15px;
  }

  hr {
    position: relative;
    top: 15px;
    margin-bottom: 15px;
    border: .5px solid white;
  }

  .todoWrapper {
    width: 100%;
    max-width: 400px;
    height: 500px;
    background-color: rgba(65, 66, 136, 0.7);
    padding: 15px;
    border-radius: 4px;
    color: white;
    box-shadow: 0 2px 10px 0 rgba(0, 0, 0, 0.29);
    overflow: scroll;
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
    cursor: pointer;
    color: #FC440F;
    margin: 0 5px;
  }

  .editButton {
    cursor: pointer;
    color: #FDE74C;
    margin: 0 5px;
  }

  .checkCircle {
    color: #85CB33;
  }

  .editToDos {
    margin: 5px 0;
    width: 100%;
    display: flex;
    justify-content: flex-end;
  }

  .editDone {
    color: #85CB33;
    cursor: pointer;
  }

  .abortEdit {
    color: #FC440F;
    cursor: pointer;
  }

  .md-tooltip {
    color: white;
    background-color: rgba(0,0,0, 0.8);
  }

  .emptyTodos {
    text-align: center;
    background-color: rgba(0,0,0, 0.5);
    border-radius: 3px;
    box-shadow: 0 2px 10px 0 rgba(0, 0, 0, 0.29);
    padding: 20px;
  }
</style>
