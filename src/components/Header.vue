<template>
  <header>
    <h1>{{ title }}</h1>
    <Button
      @toggle-add-task="$emit('toggle-add-task')"
      :color="showAddTask ? 'red' : 'green'"
      :text="showAddTask ? 'Close' : 'Add task'"
    />
  </header>
</template>


<script>
import Button from "./Button.vue";

export default {
  name: "Header",
  props: {
    title: String,
    showAddTask: Boolean,
  },

  components: {
    Button,
  },

  emits: ["toggle-add-task"],
};
</script>


<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
  padding: 10px;
}
</style>