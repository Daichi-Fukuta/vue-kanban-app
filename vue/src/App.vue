<template>
  <div>
    <div class="task-area">
      <div class="open">
        <div>
          <span>未対応</span>
          <span>{{ tasks.length }}</span>
        </div>
        <div v-for="task in tasks" v-bind:key="task.name">
          <div class="task">
            <p class="task-name">{{ task.name }}</p>
            <div>
              <span class="task-assignee">{{ task.assignee }}</span>
              <span class="task-mandays">{{ task.mandays }}人日</span>
              <div class="change-status">
                <span class="status-down">👎</span>
                <span class="status-up">👍</span>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="doing">
        <p>test</p>
      </div>
        <div class="closed">
          <p>test</p>
      </div>
    </div>
  </div>
</template>

<script>

export default ({
  data: function () {
    return {
      tasks: [
        { name: 'Task1', status: 1, assignee: '🐱', mandays: 1 },
        { name: 'Task2', status: 1, assignee: '🐶', mandays: 1 },
        { name: 'Task3', status: 2, assignee: '🐯', mandays: 2 },
        { name: 'Task4', status: 2, assignee: '🐹', mandays: 2 },
        { name: 'Task5', status: 3, assignee: '🐰', mandays: 3 },
      ],
    }
  },
})
</script>

<style scoped>
.task-area {
  display: flex;
  padding-top: 80px;
  padding-left: 170px;
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
  border-top: 1px solid rgb(124, 124, 124);
  border-bottom: 1px solid rgb(124, 124, 124);
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
