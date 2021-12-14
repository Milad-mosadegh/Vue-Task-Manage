<template>
  <div class="container">
    <Header
      @toggle-add-task="toogleAddTask"
      title="Task Tracker"
      :showAddTask="showAddTask"
    />
    <div v-if="showAddTask">
      <AddTask @add-task="addTask" />
    </div>
    <Tasks
      @toggle-reminder="toggleReminder"
      @delete-task="deleteTask"
      :tasks="tasks"
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
      tasks: [],
      showAddTask: true,
    };
  },

  methods: {
    toogleAddTask() {
      this.showAddTask = !this.showAddTask;
    },
    addTask(data) {
      this.tasks = [...this.tasks, data];
    },
    deleteTask(id) {
      if (confirm("Are you sure?")) {
        this.tasks = this.tasks.filter((x) => x.id !== id);
      }
    },

    toggleReminder(id) {
      console.log(id);
      this.tasks = this.tasks.map((x) =>
        x.id == id ? { ...x, reminder: !x.reminder } : x
      );
    },

    async fetchTasks() {
      const res = await fetch("api/tasks");
      const data = await res.json();
      return data;
    },

    async fetchOneTask(id) {
      const res = await fetch(`api/tasks/${id}`);
      const data = await res.json();
      return data;
    },
  },

  async created() {
    this.tasks = await this.fetchTasks();
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.container {
  margin: 0 auto;
  width: 80%;
  padding: 20px;
  border: 1px solid blueviolet;
}
</style>
