<template>
  <div class="task" @dblclick="$emit('toggle-reminder')">
    <div :class="[task.reminder ? 'reminder' : '']"></div>
    <div class="title">
      <h3>{{ task.text }}</h3>
      <i class="fa fa-times red" @click="$emit('delete-task')"></i>
    </div>
    <p>{{ task.time }}</p>
  </div>
</template>

<script>
export default {
  name: "Task",
  props: {
    task: Object,
  },
};
</script>

<style scoped>
h3 {
  margin-bottom: 5px;
}

.title {
  display: flex;
  justify-content: space-between;
}

.red {
  color: rgb(122, 32, 32);
}

.task {
  position: relative;
  margin: 0;
  background-color: rgba(42, 42, 42, 0.1);
  padding: 15px;
  border-radius: 5px;
  cursor: pointer;
}

.reminder {
  background-color: rgb(0, 168, 8);
  width: 4px;
  height: 100%;
  position: absolute;
  left: 0.5px;
  top: 0;
  border-radius: 5px;
}
</style>
