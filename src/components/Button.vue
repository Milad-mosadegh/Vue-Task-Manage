<template >
  <button @click="onClick()" :style="{ backgroundColor: color }" class="btn">
    {{ text }}
  </button>
</template>

<script>
export default {
  name: "Button",
  props: {
    text: String,
    color: String,
  },
  methods: {
    onClick() {
      console.log("ADD TASKS");
      this.$emit("toggle-add-task");
    },
  },
};
</script> 


<style scoped>
.btn {
  background-color: #222;
  color: white;
  border: none;
  border-radius: 5px;
  padding: 10px;
}
</style>