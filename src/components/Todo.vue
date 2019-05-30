<template>
  <div class="todo">
    <input
      class="add-input"
      type="text"
      autofocus="autofocus"
      placeholder="what's to do next ?"
      @keyup.enter="addTodo"
    >
    <section class="container">
      <TodoItems
      :todo="todo"
      v-for="(todo, index)
      in filterTodos"
      :key="index"
      @deleteTodo="deleteTodo"
      >
    </TodoItems>
    </section>
    <TodoTabs
      :todos="todos"
      :filter="filter"
      @toggle="toggleFilter"
      @clearAllCompleted="clearAllCompleted"
    >
    </TodoTabs>
  </div>
</template>

<script>
import TodoItems from './TodoItems'
import TodoTabs from './TodoTabs'

if (!localStorage.hasOwnProperty('todos')) {
  localStorage.setItem('todos', '[]')
}

let todoList = JSON.parse(localStorage.getItem('todos'))

export default {
  name: 'Todo',
  components: {
    TodoItems,
    TodoTabs
  },
  data() {
    return {
      id: 0,
      todos: todoList,
      filter: '全部'
    }
  },
  watch: {
    'todos': {
      handler() {
        localStorage.setItem('todos', JSON.stringify(this.todos))
      },
      deep: true
    }
  },
  computed: {
    filterTodos() {
      if (this.filter === '全部') {
        return this.todos
      }
      const completed = this.filter === '已完成'
      return this.todos.filter(todo => completed === todo.completed)
    }
  },
  methods: {
    addTodo(e) {
      if (e.target.value === '') {
        alert('还没想好做什么吗？')
        return false
      }
      this.todos.unshift({
        id: this.id++,
        content: e.target.value.trim(),
        completed: false
      })
      e.target.value = ''
    },
    deleteTodo(id) {
      this.todos.splice(this.todos.findIndex(todo => todo.id === id), 1)
    },
    toggleFilter(state) {
      this.filter = state
    },
    clearAllCompleted() {
      this.todos = this.todos.filter(todo => (todo = !todo.completed))
    }
  }
}
</script>

<style scoped>
h1,h2 {
  font-weight: normal;
}

.todo {
  /* display: flex;
  justify-content: center;
  align-items: center; */
  max-width: 600px;
  /* border-radius: 10px;
  box-shadow: 0 0px 1px rgba(0, 0, 0, 0.5), 0 1px 2px rgba(0, 0, 0, 0.48); */
}

.add-input {
  width: 100%;
  color: inherit;
  font-size: 24px;
  line-height: 1.4em;
  outline: none;
  border: 1px solid #999;
  border-radius: 5px;
  box-shadow: 0 0px 1px rgba(0, 0, 0, 0.48);
  box-sizing: border-box;
  padding: 16px 30px;
  margin-bottom: 20px;
}

.container {
  min-height: 200px;
  border: 1px solid #999;
  border-radius: 5px;
  box-shadow: 0 0px 1px rgba(0, 0, 0, 0.48);
  box-sizing: border-box;
}
</style>
