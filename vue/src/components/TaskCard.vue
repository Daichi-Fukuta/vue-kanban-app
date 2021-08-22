<template>
  <div class="card">
    <div class="card-content">
      {{ task.name }}
    </div>
    <footer class="card-footer">
      <div class="card-footer-item">
        {{ task.assignee }}
      </div>
      <div class="card-footer-item">
        {{ task.mandays }} 人日
      </div>
    </footer>
    <footer class="card-footer">
      <a class="card-footer-item" v-on:click="decrementStatus(task)">◀︎</a>
      <a class="card-footer-item" v-on:click="incrementStatus(task)">▶︎</a>
    </footer>
  </div>
</template>

<script>
export default {
  props: ['task'],
  methods: {
    incrementStatus: function (task) {
      if (1 <= task.status && task.status <= 2) {
        task.status++
      }
    },
    decrementStatus: function (task) {
      if (2 <= task.status && task.status <=3) {
        task.status--
      }
    }
  }
}
</script>