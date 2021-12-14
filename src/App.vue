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

    <Footer />
  </div>
</template>


<script>
import Header from "./components/Header.vue";
import Tasks from "./components/Tasks.vue";
import AddTask from "./components/AddTask.vue";
import Footer from "./components/Footer.vue";

export default {
  name: "App",
  components: {
    Header,
    Tasks,
    AddTask,
    Footer,
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

    // Add Method To UI and Json Backend
    async addTask(task) {
      const res = await fetch("api/tasks", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(task),
      });
      const data = await res.json();
      this.tasks = [...this.tasks, data];
    },

    // Delete Method from UI and Json Backend
    async deleteTask(id) {
      if (confirm("Are you sure?")) {
        const res = await fetch(`api/tasks/${id}`, {
          method: "DELETE",
        });

        res.status === 200
          ? (this.tasks = this.tasks.filter((x) => x.id !== id))
          : alert("Error Deleting Task");
      }
    },

    async toggleReminder(id) {
      const taskToToggle = await this.fetchOneTask(id);
      const updTask = {
        ...taskToToggle,
        reminder: !taskToToggle.reminder,
      };

      const res = await fetch(`api/tasks/${id}`, {
        method: "PUT",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(updTask),
      });

      const data = await res.json();
      this.tasks = this.tasks.map((x) =>
        x.id == id ? { ...x, reminder: data.reminder } : x
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
