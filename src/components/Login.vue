<template>
  <div id="login">
    <h1>Login</h1>
    <div class="form-inputs">
      <v-text-field label="Phone Number" type="text" id="username" name="username" v-model="input.username" placeholder="Phone Number" />
    </div>
    <div class="form-inputs">
      <v-text-field label="Password" type="password" id="password" name="password" v-model="input.password" placeholder="Password" />
    </div>
    <v-btn type="button" v-on:click="login()">Login</v-btn>
    <p class="forgot-password text-right">
      Already have an account
      <router-link to="/register">Register</router-link>
    </p>
  </div>
</template>

<script>
import axios from 'axios';
import Home from "@/components/Home";
import Register from "@/components/Register";
export default {
  name: 'Login',
  data() {
    return {
      input: {
        username: "",
        password: ""
      }
    }
  },
  methods: {
    login() {
      if(this.input.username != "" && this.input.password != "") {
        // This should actually be an api call not a check against this.$parent.mockAccount
        const url = "http://localhost:8090/auth/authenticate" //give suitable appi url
        axios({
          method: 'post',
          url: url,
          data: this.input
        }).then((response) => {
          console.log("Got response from server");
          console.log(response)
          if(response.data.code=='0'){
            this.goToMainPage();
          } else {
            this.goToRegisterPage();
          }
        })
      } else {
        console.log("A Phone Number and password must be present");
      }
    },
    goToMainPage(){
      this.routeToPage('/home', Home);
    },
    goToRegisterPage(){
      this.routeToPage('/register', Register);
    },
    routeToPage(path, component){
      this.$router.push({ path: path, component:component })
    }
  }
}
</script>

<style>
#login .form-inputs {
  padding-bottom: 10px;
}
#login .form-inputs label {
  padding-right: 10px;
}
</style>