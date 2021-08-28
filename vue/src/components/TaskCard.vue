<template>
  <div class="task">
    <p class="task-name">{{ task.name }}</p>
    <div>
      <span class="task-assignee">{{ task.assignee }}</span>
      <span class="task-mandays">{{ task.mandays }}人日</span>
      <div class="change-status">
        <span class="status-down" @click="statusDown(task)">◀</span>
        <span class="status-up" @click="statusUp(task)">▶</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['task'],
  methods: {
    statusDown: function (task) {
      if (task.status !== 1) {
        task.status -= 1;
      }
    },
    statusUp: function (task) {
      if (task.status !== 3) {
        task.status += 1;
      }
    }
  }
}
</script>

<style scoped>
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
  font-size: 26px;
  color: rgb(32, 141, 214);
}
.status-up {
  display: inline-block;
  width: 150px;
  text-align: center;
  margin-top: 3px;
  margin-bottom: 3px;
  font-size: 26px;
  color: rgb(32, 141, 214);
}
</style>
