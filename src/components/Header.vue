<template>
  <div>
    <h1>{{ title }}</h1>
    <CustomButton text="Add Task" @click="$emit('add-task-display')" />
  </div>
</template>

<script>
import CustomButton from "./CustomButton.vue";

export default {
  name: "Header",
  props: {
    title: String,
  },
  components: {
    CustomButton,
  },
};
</script>

<style scoped>
div {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 15px 15px;
}
h1 {
  font-weight: 900;
}
</style>
