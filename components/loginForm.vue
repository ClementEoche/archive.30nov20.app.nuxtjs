<template>
  <div class="content-inputs">
    <vs-input class="mb-4" v-model="usernameInput" label="Username" placeholder="" style="margin-bottom: 20px"/>
    <vs-input type="password" class="mb-4" v-model="passwordInput" label="Password" placeholder=""
              style="margin-bottom: 20px"/>
    <vs-button flat dark @click="login">
      Login
    </vs-button>
  </div>
</template>

<script>
export default {
  name: "LoginForm",
  data: () => ({
    usernameInput: '',
    passwordInput: '',
  }),
  methods: {
    async login() {
      var self = this
      await this.$axios.$post('/api/auth/signin', {
        "username": this.usernameInput,
        "password": this.passwordInput
      })
        .then(function (response) {
          console.log(response)
          localStorage.setItem('jwt', response.accessToken)
          self.$nuxt.$router.replace({ path: '/' })
        })
        .catch(function (error) {
          console.log(error);
          self.error = "login or password incorrect."
        });
    }
  }
}
</script>

<style scoped>

</style>
