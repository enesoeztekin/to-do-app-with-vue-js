<template>
  <div class="main">
    <Header title="TO-DOO" @add-task-display="AddTaskDisplay" />
    <AddTask
      :display="[this.display ? 'addTask' : 'invisible']"
      @add-task="addTask"
    />
    <Tasks
      :tasks="tasks"
      @delete-task="deleteTask"
      @toggle-reminder="toggleReminder"
    />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Tasks from "./components/Tasks.vue";
import AddTask from "./components/AddTask.vue";

export default {
  name: "App",
  components: {
    Header,
    Tasks,
    AddTask,
  },
  data() {
    return {
      display: false,
      tasks: [],
    };
  },
  methods: {
    async addTask(task) {
      const res = await fetch("http://localhost:3000/tasks", {
        method: "POST",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(task),
      });
      const data = res.json();
      this.tasks = [...this.tasks, data];
    },
    async deleteTask(id) {
      const res = await fetch(`http://localhost:3000/tasks/${id}`, {
        method: "DELETE",
      });

      res.status === 200
        ? (this.tasks = this.tasks.filter((task) => task.id != id))
        : alert("Error while deleting the task!");
    },
    async toggleReminder(id) {
      const taskToToggle = await this.fetchTask(id);
      const updReminder = { ...taskToToggle, reminder: !taskToToggle.reminder };

      const res = await fetch(`http://localhost:3000/tasks/${id}`, {
        method: "PUT",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(updReminder),
      });

      const data = res.json();

      var index = this.tasks.findIndex((task) => task.id == id);
      this.tasks[index].reminder ? (this.tasks[index].reminder = data.reminder) : (this.tasks[index].reminder = !data.reminder);
    },
    AddTaskDisplay() {
      this.display ? (this.display = false) : (this.display = true);
    },
    async fetchTasks() {
      const res = await fetch("http://localhost:3000/tasks");
      const data = res.json();
      return data;
    },
    async fetchTask(id) {
      const res = await fetch(`http://localhost:3000/tasks/${id}`);
      const data = res.json();
      return data;
    },
  },
  async created() {
    this.tasks = await this.fetchTasks();
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  /* outline: 1px solid salmon; */
}

body {
  margin: 12px;
}

.main {
  border: 1px solid black;
}
</style>
