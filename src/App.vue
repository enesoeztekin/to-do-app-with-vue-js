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
    addTask(task) {
      this.tasks = [...this.tasks, task];
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => task.id != id);
    },
    toggleReminder(id) {
      var index = this.tasks.findIndex((task) => task.id == id);
      this.tasks[index].reminder
        ? (this.tasks[index].reminder = false)
        : (this.tasks[index].reminder = true);
    },
    AddTaskDisplay() {
      this.display ? (this.display = false) : (this.display = true);
    },
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: "Do your laundry!",
        time: "11th Nov 2021 at 3:14 PM",
        reminder: true,
      },
      {
        id: 2,
        text: "Practice in English.",
        time: "11th Nov 2021 at 3:14 PM",
        reminder: true,
      },
      {
        id: 3,
        text: "Sleep before midnight!",
        time: "11th Nov 2021 at 3:14 PM",
        reminder: false,
      },
      {
        id: 4,
        text: "Go to work!",
        time: "11th Nov 2021 at 3:14 PM",
        reminder: false,
      },
      {
        id: 5,
        text: "Practice with the guitar.",
        time: "11th Nov 2021 at 3:14 PM",
        reminder: false,
      },
    ];
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
