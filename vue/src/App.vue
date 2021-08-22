<template>
  <section class="section" id="app">
    <div class="container">
      <input type="text" v-model="newTaskName">
      <select v-model="newTaskAssignee">
        <option value="🐱">🐱</option>
        <option value="🐶">🐶</option>
        <option value="🐹">🐹</option>
      </select>
      <input type="number" v-model="newTaskMandays">
      <button v-on:click="addTask">追加</button>
      <hr>
      <div class="columns">
        <div class="column status-1">
          <div class="tags has-addons">
            <span class="tag">未対応</span>
            <span class="tag is-dark">{{ tasksOpen.length }}</span>
          </div>
          <transition-group name="fade">
            <task-card v-bind:task="task" v-for="task in tasksOpen" v-bind:key="task.name"></task-card>
          </transition-group>
        </div>
        <div class="column status-2">
          <div class="tags has-addons">
            <span class="tag">処理中</span>
            <span class="tag is-dark">{{ tasksDoing.length }}</span>
          </div>
          <transition-group name="fade">
            <task-card v-bind:task="task" v-for="task in tasksDoing" v-bind:key="task.name"></task-card>
          </transition-group>
        </div>
        <div class="column status-3">
          <div class="tags has-addons">
            <span class="tag">完了</span>
            <span class="tag is-dark">{{ tasksClosed.length }}</span>
          </div>
          <transition-group>
            <task-card v-bind:task="task" v-for="task in tasksClosed" v-bind:key="task.name"></task-card>
          </transition-group>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
var filters = {
  open: function (tasks) {
    return tasks.filter(function (task) {
      return task.status === 1
    })
  },
  doing: function (tasks) {
    return tasks.filter(function (task) {
      return task.status === 2
    })
  },
  closed: function (tasks) {
    return tasks.filter(function (task) {
      return task.status === 3
    })
  }
}

import TaskCard from './components/TaskCard';

export default {
  name: 'App',
  components: {
    TaskCard: TaskCard,
  },
  data() {
    return {
      // status => 1: 未対応 2: 処理中 3: 完了
      tasks: [
        { name: 'task 1', status: 1, assignee: '🐱', mandays: 3 },
        { name: 'task 2', status: 1, assignee: '🐶', mandays: 2 },
        { name: 'task 3', status: 2, assignee: '🐱', mandays: 1 },
        { name: 'task 4', status: 3, assignee: '🐹', mandays: 1 }
      ],
      newTaskName: '',
      newTaskAssignee: null,
      newTaskMandays: 0,
    }
  },
  computed: {
    tasksOpen: function () {
      return filters.open(this.tasks);
    },
    tasksDoing: function () {
      return filters.doing(this.tasks);
    },
    tasksClosed: function () {
      return filters.closed(this.tasks);
    }
  },
  methods: {
    addTask: function () {
      this.tasks.push({
        name: this.newTaskName,
        status: 1,
        assignee: this.newTaskAssignee,
        mandays: this.newTaskMandays,
      })
    }
  }
}
</script>

<style scoped>
  .status-1 {
    background-color: #ed8077;
  }
  .status-2 {
    background-color: #4488c5;
  }
  .status-3 {
    background-color: #5eb5a6;
  }
  .card {
    margin-bottom: 5px;
  }
  .card-footer-item {
    padding-top: 0px;
    padding-bottom: 0px;
  }
  .fade-enter-active, .fade-leave-active {
  transition: opacity 0.7s
  }
  .fade-enter, .fade-leave-to {
    opacity: 0
  }
</style>