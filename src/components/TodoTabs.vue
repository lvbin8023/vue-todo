<template>
  <div class="helper">
    <span class="left">{{unfinishedTodoLength}}项任务未完成</span>
    <span class="tabs">
      <span
        :class="['middle',filter === state ? 'actived' : '']"
        v-for="state in states"
        :key="state"
        @click="toggleFilter(state)"
      >{{state}}</span>
    </span>
    <span class="clear" @click.prevent="clearAllCompleted">清除所有已完成</span>
  </div>
</template>

<script>
export default {
  props: {
    todos: {
      type: Array,
      required: true
    },
    filter: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      states: ['全部', '未完成', '已完成']
    }
  },
  computed: {
    unfinishedTodoLength() {
      return this.todos.filter(todo => !todo.completed).length
    }
  },
  methods: {
    toggleFilter(state) {
      this.$emit('toggle', state)
    },
    clearAllCompleted() {
      this.$emit('clearAllCompleted')
    }
  }
}
</script>

<style scoped>
.helper {
  display: flex;
  justify-content: space-between;
  font-size: 20px;
  font-weight: 400;
  line-height: 30px;
  padding: 5px 0;
  margin-top: 15px;
}

.left
.tabs,
.clear {
  padding: 0 5px;
}

.tabs {
  width: 200px;
  display: flex;
  justify-content: space-between;
}

.tabs .middle.actived {
  display: inline-block;
  border: 1px solid #bd3737;
  border-radius: 5px;
  padding: 0 5px;
  cursor: pointer;
}

.clear {
  cursor: pointer;
}
</style>
