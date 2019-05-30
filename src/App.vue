<template>
  <div id="app">
    <Header></Header>
    <Todo></Todo>
  </div>
</template>

<script>
import Header from './components/Header'
import Todo from './components/Todo'

export default {
  name: 'App',
  components: {
    Header,
    Todo
  }
}
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.header {
  margin: 0 auto 30px;
}

.todo {
  margin: 0 auto;
}
</style>
