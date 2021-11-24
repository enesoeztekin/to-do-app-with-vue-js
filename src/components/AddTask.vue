<template>
  <div :class="display">
    <form @submit="onSubmit">
      <label for="text">Task Title</label>
      <input
        type="text"
        placeholder="Enter a task title."
        v-model="taskTitle"
      />
      <label for="date">Date of Task</label>
      <input
        type="datetime"
        placeholder="Enter a task date."
        v-model="taskDate"
      />
      <div class="align">
        <label for="checkbox">Set Reminder:</label>
        <input type="checkbox" v-model="reminder" />
        <input type="submit" value="Add Task" />
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "AddTask",
  props: {
    display: {
      type: String,
      default: "addTask",
    },
  },
  data() {
    return {
      taskTitle: "",
      taskDate: "",
      reminder: false,
    };
  },
  methods: {
    onSubmit(e) {
      e.preventDefault();
      if (!this.taskTitle) {
        alert("Please enter a task title.");
        return;
      }

      // eslint-disable-next-line no-unused-vars
      const newTask = {
        id: Math.floor(Math.random() * 10000),
        text: this.taskTitle,
        time: this.taskDate,
        reminder: this.reminder,
      };

      this.taskTitle = "";
      this.taskDate = "";
      this.reminder = false;

      this.$emit("add-task", newTask);
    },
  },
};
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.invisible {
  display: none;
}
.addTask {
  display: flex;
  justify-content: center;
  align-items: center;
}
label {
  display: block;
}
input {
  display: block;
  border: 1px solid black;
  background-color: none;
  border-radius: 5px;
  height: 25px;
  width: 100%;
  padding: 0 10px;
}
input {
  margin-bottom: 10px;
}
input[type="submit"] {
  width: max-content;
  border: 0;
  border-radius: 5px;
  background-color: rgba(0, 0, 0, 1);
  color: white;
  margin-left: auto;
  padding: 5px 15px;
  margin-top: 5px;
}

form {
  margin: 0 15px;
  width: 100%;
}

label[for="checkbox"],
input[type="checkbox"] {
  display: inline-block;
  width: max-content;
}

input[type="checkbox"] {
  margin: 16px 10px;
  width: 15px;
}

.align {
  display: flex;
  align-items: center;
}
</style>
