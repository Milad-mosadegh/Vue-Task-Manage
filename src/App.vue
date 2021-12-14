<template>
  <div class="container">
    <Header
      @toggle-add-task="toogleAddTask"
      title="Task Tracker"
      :showAddTask="showAddTask"
    />

    <router-view :showAddTask="showAddTask"></router-view>

    <Footer />
  </div>
</template> 


<script>
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";

export default {
  name: "App",
  components: {
    Header,
    Footer,
  },

  data() {
    return {
      showAddTask: true,
    };
  },

  methods: {
    toogleAddTask() {
      this.showAddTask = !this.showAddTask;
    },
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
