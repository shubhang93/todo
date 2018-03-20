<template>
  <div id="app">
    <AppContainer/>
  </div>
</template>

<script>
  import HelloWorld from './components/HelloWorld'
  import AppContainer from './components/AppContainer'

  export default {
    name: 'App',
    components: {
      AppContainer
    }
  }
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
    display: flex;
    justify-content: center;
  }
</style>
