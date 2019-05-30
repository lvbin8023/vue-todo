<template>
  <div :class="['todo-item',todo.completed ? 'completed' : '']">
    <input type="checkbox" class="toggle" v-model="todo.completed">
    <label class="label">{{todo.content}}</label>
    <button class="delete" @click.prevent="deleteTodo(todo.id)"></button>
  </div>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true
    }
  },
  methods: {
    deleteTodo(id) {
      this.$emit('deleteTodo', id)
    }
  }
}
</script>

<style scoped>
.todo-item {
  position: relative;
  font-size: 20px;
  outline: none;
}

.todo-item .toggle {
  width: 50px;
  height: 30px;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  text-align: center;
  margin: auto 0;
  border: none;
  outline: none;
  appearance: none;
}

.todo-item .toggle::after {
  content: url("../assets/img/round.svg");
}

.todo-item .toggle:checked::after {
  content: url("../assets/img/done.svg");
}

.todo-item.completed {
  color: #d9d9d9;
  text-decoration: line-through;
}

.todo-item .label {
  font-size: 22px;
  white-space: pre-line;
  word-break: break-all;
  padding: 15px 60px 15px 15px;
  margin-left: 45px;
  display: block;
  line-height: 1.2;
  text-align: left;
}

.todo-item .delete {
  position: absolute;
  top: 0;
  bottom: 0;
  right: 0;
  margin: auto 0;
  width: 40px;
  height: 40px;
  font-size: 30px;
  color: #cc9a9a;
  outline: none;
  appearance: none;
  border-width: 0;
  transition: 0.2s ease-out;
  background-color: transparent;
}

.todo-item:hover .delete::after {
  content: "x";
  cursor: pointer;
}
</style>
