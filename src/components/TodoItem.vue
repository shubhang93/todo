<template>
  <div class="todo-container">
    <p class="todo-text" v-bind:class="[todoItem.isComplete?'todo-text-completed':'']"
       v-on:click="toggleTask($event,todoItem.id)">{{todoItem.text}}</p>
    <p class="delete-button" v-on:click="deleteTask($event,todoItem.id)">&#10006</p>
  </div>
</template>

<script>
  export default {
    name: "todo-item",
    props: {
      todoItem: {
        text: String,
        id: Number,
        isComplete: Boolean
      }
    },
    methods: {
      toggleTask: function (e, id) {
        this.$emit('toggle', id)
      },

      deleteTask: function (e, id) {
        this.$emit('delete', id)
      }
    }

  }
</script>

<style scoped>
  .todo-container {
    display: flex;
    height: 50px;
    align-items: center;
    justify-content: center;
  }

  .todo-text {
    color: burlywood;
    font-family: "Noto Mono";
  }

  .delete-button {
    margin-left: 40px;
  }

  .todo-text-completed {
    text-decoration: line-through;
  }

</style>
