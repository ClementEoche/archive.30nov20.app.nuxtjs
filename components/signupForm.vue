<template>
  <div class="content-inputs">
    <vs-input class="mb-4" v-model="usernameInput" label="Username" placeholder="" style="margin-bottom: 20px"/>
    <vs-input class="mb-4" v-model="emailInput" label="Email" placeholder="" style="margin-bottom: 20px"/>
    <vs-input type="password" class="mb-4" v-model="passwordInput" label="Password" placeholder=""
              style="margin-bottom: 20px"/>
    <vs-button flat dark @click="signup">
      Signup
    </vs-button>
  </div>
</template>

<script>
export default {
  name: "signupForm",
  data: () => ({
    usernameInput: '',
    emailInput: '',
    passwordInput: '',
  }),
  methods: {
    async signup() {
      var self = this
      await this.$axios.$post('/api/auth/signup', {
        "username": this.usernameInput,
        "email": this.emailInput,
        "password": this.passwordInput,
        "roles":["user"]
      })
        .then(function () {
          self.$nuxt.$router.replace({ path: '/' })
        })
        .catch(function (error) {
          console.log(error);
          self.error = "signup error"
        });
    }
  }
}
</script>

<style scoped>

</style>
