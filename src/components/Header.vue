<template>
  <div class="header">
    <h1>{{ msg }}</h1>
  </div>
</template>

<script>
export default {
  name: 'Header',
  data() {
    return {
      msg: 'Todo List'
    }
  }
}
</script>

<style scoped>
h1,
h2 {
  font-weight: normal;
}

.header {
  display: flex;
  justify-content: center;
  align-items: center;
  max-width: 400px;
  width: 100%;
  background: #41B883;
  border-radius: 10px;
  box-shadow: 0 0px 1px rgba(0, 0, 0, 0.5), 0 1px 2px rgba(0, 0, 0, 0.48);
}
</style>
