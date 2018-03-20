<template>
  <div>
    <h1>Todo App using Vue and Clojure</h1>
    <TodoItem v-for="todoItem in todos" :todoItem="todoItem" v-on:toggle="toggleTodo"
              v-on:delete="deleteTask" :key="todoItem.id"></TodoItem>
    <input type="text" class="todo-input" @keyup.enter="addTask" v-model="text">
    <button v-on:click="saveTodos" class="save-button">Save</button>
  </div>
</template>


<script>
  import TodoItem from './TodoItem'

  export default {
    name: "app-container",
    components: {
      TodoItem
    },
    data: function () {
      return {todos: [], text: ''}
    },
    mounted: function () {
      this.refreshTasks()
    },
    methods: {

      refreshTasks: function () {
        fetch('http://localhost:3000/todo/all').then(resp => resp.json())
          .then(todos => this.todos = todos)
      },


      toggleTodo: function (todoid) {
        this.todos = this.todos.map(todo =>
          todo.id === todoid ? ({...todo, isComplete: !todo.isComplete}) : todo
        )
      },
      addTask: function () {
        if (this.text) {
          this.todos = this.todos.concat({
            id: new Date().getTime(),
            text: this.text,
            isCompleted: false
          })
          fetch('http://localhost:3000/todo/add', {
            method: 'POST',
            body: JSON.stringify({text: this.text}),
            headers: {
              'Content-Type': 'application/json'
            }
          }).then(r => console.log({r}))
        }
      },
      deleteTask: function (id) {
        this.todos = this.todos.filter(todo => todo.id !== id)
        fetch(`http://localhost:3000/todo/${id}`, {method: 'DELETE'}).then(r => console.log({r}))
      },

      saveTodos: function () {

      }
    }
  }
</script>

<style scoped>
  .todo-input {
    border-color: burlywood;
    border-width: 1px;
    border-style: solid;
  }

  .save-button {
    border-color: burlywood;
    background-color: transparent;
    border-style: solid;
    border-width: 1px;
    width: 100px;
    font-family: "Noto Mono";
    color: burlywood;
  }

  .save-button:active {
    background-color: burlywood;
    color: white;
    border: none;
  }

</style>
