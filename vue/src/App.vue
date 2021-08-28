<template>
  <div>
    <div>
      <span>タスク: </span>
      <input type="text" v-model="newTaskName">
      <span>担当者: </span>
      <input type="text" v-model="newTaskAssignee">
      <span>人日:</span>
      <input type="number" v-model="newTaskMandays">
      <button @click="addTask">追加</button>
    </div>
    <div class="task-area">
      <div class="open">
        <div class="status">
          <span class="status-name">未対応</span>
          <span class="status-count">{{ openTasks.length }}</span>
        </div>
        <task-card v-bind:task="task" v-for="task in openTasks" v-bind:key="task.name"></task-card>
      </div>
      <div class="doing">
        <div class="status">
          <span class="status-name">処理中</span>
          <span class="status-count">{{ doingTasks.length }}</span>
        </div>
        <task-card v-bind:task="task" v-for="task in doingTasks" v-bind:key="task.name"></task-card>
      </div>
        <div class="closed">
        <div class="status">
          <span class="status-name">完了</span>
          <span class="status-count">{{ closedTasks.length }}</span>
        </div>
        <task-card v-bind:task="task" v-for="task in closedTasks" v-bind:key="task.name"></task-card>
      </div>
    </div>
  </div>
</template>

<script>
let status_filter = {
  open: function (tasks) {
    return tasks.filter(function (task) {
      return task.status === 1;
    });
  },
  doing: function (tasks) {
    return tasks.filter(function (task) {
      return task.status === 2;
    });
  },
  closed: function (tasks) {
    return tasks.filter(function (task) {
      return task.status === 3;
    });
  }
}

import TaskCard from './components/TaskCard.vue';

export default ({
  components: {
    TaskCard: TaskCard,
  },
  data: function () {
    return {
      tasks: [
        { name: 'Task1', status: 1, assignee: '🐱', mandays: 1 },
        { name: 'Task2', status: 1, assignee: '🐶', mandays: 1 },
        { name: 'Task3', status: 2, assignee: '🐯', mandays: 2 },
        { name: 'Task4', status: 2, assignee: '🐹', mandays: 2 },
        { name: 'Task5', status: 3, assignee: '🐰', mandays: 3 },
      ],
      newTaskName: '',
      newTaskAssignee: '',
      newTaskMandays: null,
    }
  },
  computed: {
    openTasks: function () {
      return status_filter.open(this.tasks);
    },
    doingTasks: function () {
      return status_filter.doing(this.tasks);
    },
    closedTasks: function() {
      return status_filter.closed(this.tasks);
    }
  },
  methods: {
    addTask: function () {
      this.tasks.push(
        {
          name: this.newTaskName,
          status: 1,
          assignee: this.newTaskAssignee,
          mandays: this.newTaskMandays,
        }
      )
    }
  }
})
</script>

<style scoped>
.task-area {
  display: flex;
  padding-top: 80px;
  padding-left: 170px;
}
.status {
  padding: 10px;
}
.status-name {
  background-color: rgb(212, 212, 212);
  font-size: 12px;
  border-top-left-radius: 5px;
  border-bottom-left-radius: 5px;
  padding: 7px;
}
.status-count {
  background-color: rgb(66, 66, 66);
  color: #fff;
  font-size: 12px;
  border-top-right-radius: 5px;
  border-bottom-right-radius: 5px;
  padding: 7px;
}
.task {
  width: 300px;
  height: 120px;
  background-color: rgb(240, 240, 240);
  margin: 10px auto;
  border-radius: 10px;
  box-shadow: 5px 5px 15px rgb(77, 77, 77);
}
.task-name {
  padding: 5px;
}
.task-assignee {
  padding: 10px;
}
.task-mandays {
  padding: 10px;
}
.change-status {
  border-top: 0.5px solid rgb(124, 124, 124);
  border-bottom: 0.5px solid rgb(124, 124, 124);
}
.status-down {
  display: inline-block;
  width: 150px;
  text-align: center;
  margin-top: 3px;
  margin-bottom: 3px;
}
.status-up {
  display: inline-block;
  width: 150px;
  text-align: center;
  margin-top: 3px;
  margin-bottom: 3px;
}
.open {
  width: 500px;
  height: 800px;
  background-color: rgb(206, 67, 67);
}
.doing {
  width: 500px;
  height: 800px;
  background-color: rgb(79, 104, 172);
}
.closed {
  width: 500px;
  height: 800px;
  background-color: rgb(87, 170, 159);
}
</style>
