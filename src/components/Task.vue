<template>
  <div
    @dblclick="$emit('toggle-reminder')"
    :class="[task.reminder ? 'reminder' : '', 'task']"
  >
    <h3>
      {{ task.text }}
      <i @click="$emit('delete-task', task.id)" class="fas fa-times"></i>

      <!-- <Button color="red" text="X" /> -->
    </h3>
    <p>{{ task.day }}</p>
  </div>
</template>

<script>
import Button from "./Button.vue";
export default {
  name: "Task",
  props: {
    task: Object,
  },

  components: {
    Button,
  },
};
</script>


<style scoped>
.task {
  background: rgb(202, 201, 201);
  /* border-radius: 10px; */
}

h3 {
  display: flex;
  justify-content: space-between;
  padding: 10px;
}

.fas {
  color: red;
}
.task.reminder {
  border-left: 5px solid green;
}
</style>