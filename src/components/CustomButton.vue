<template>
  <button>{{ text }}</button>
</template>

<script>
export default {
  name: "CustomButton",
  props: {
    text: String,
  },
};
</script>

<style scoped>
button {
  background-color: rgb(0, 168, 8);
  color: white;
  border: 0;
  padding: 5px 15px;
  border-radius: 15px;
}
button:hover {
  background-color: green;
}
</style>
