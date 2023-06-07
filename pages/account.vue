<template>
  <div class="grid" style="margin-top: 100px">
    <vs-row>
      <navbar page="account"></navbar>
    </vs-row>
    <vs-row justify="center">
      <vs-col w="2">
        <h5 style="margin-bottom: 20px">Login</h5>
        <LoginForm></LoginForm>
      </vs-col>
      <vs-col w="2">
        <h5 style="margin-bottom: 20px">Signup</h5>
        <SignupForm></SignupForm>
      </vs-col>
    </vs-row>
  </div>
</template>

<script>
import Navbar from "@/components/navbar";
import LoginForm from "@/components/loginForm";
import SignupForm from "@/components/signupForm";

export default {
  name: "account",
  components: {SignupForm, LoginForm, Navbar}
}
</script>

<style scoped>

</style>
