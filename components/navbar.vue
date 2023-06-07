<template>
  <div class="center">
    <vs-navbar square text-white fixed :color="'dark'">
      <template #left>
        My CRUD client
      </template>
      <vs-navbar-item :active="page == 'home'" id="home" to="/">
        Home
      </vs-navbar-item>
      <vs-navbar-item  :active="page == 'tasks'" id="tasks" to="/tasks">
        Tasks
      </vs-navbar-item>
      <template #right>
        <vs-button  relief success id="login" to="/account">Login</vs-button>
        <vs-button  relief danger id="logout" @click="logout">Logout</vs-button>
      </template>
    </vs-navbar>
  </div>
</template>
<script>
export default {
  name: "navbar",
  data: () => ({
    connected: false
  }),
  props: ['page'],
  methods: {
    logout() {
      if (process.browser) {
        localStorage.removeItem('jwt');
        window.location = "/"
      }
    },
  },
  created() {
    if (process.browser) {
      if (localStorage.getItem('jwt')!=null) {
        this.connected = true
      }
    }
  }
}
</script>
