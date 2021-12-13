<template>
  <div v-for="x in tasks" :key="x.id">
    <Task
      @toggle-reminder="$emit('toggle-reminder', x.id)"
      @delete-task="$emit('delete-task', x.id)"
      :task="x"
    />
  </div>
</template>


<script>
import Task from "./Task.vue";

export default {
  name: "Tasks",
  props: {
    tasks: Array,
  },

  components: {
    Task,
  },

  emits: ["delete-task", "toggle-reminder"],
};
</script>