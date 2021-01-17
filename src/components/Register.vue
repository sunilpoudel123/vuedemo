<template>
  <div>
    <v-toolbar
        dark
        prominent
        src="https://cdn.vuetifyjs.com/images/backgrounds/vbanner.jpg">
      <v-app-bar-nav-icon></v-app-bar-nav-icon>
      <v-toolbar-title></v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn icon>
        <v-icon>mdi-export</v-icon>
      </v-btn>
    </v-toolbar>
    <div class="vue-template">
      <div class="hero-body">
        <div class="container">
          <form>
            <h3>Register Up</h3>
            <v-row>
              <v-col cols="4" class="d-flex child-flex">
                <div class="form-inputs">
                  <v-text-field label="Phone Number" type="text" id="phoneNumber" name="phoneNumber" v-model="input.username" placeholder="Phone Number" />
                </div>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="4" class="d-flex child-flex">
                <div class="form-inputs">
                  <v-text-field label="SMS Code" type="text" id="smscode" name="smscode" v-model="input.smscode" placeholder="SMS code" />
                </div>
              </v-col>
            </v-row>

            <v-row>
              <v-col cols="4" class="d-flex child-flex">
                <div class="form-inputs">
                  <v-text-field label="Password" type="text" id="password" name="password" v-model="input.password" placeholder="Password" />
                </div>
              </v-col>
            </v-row>
            <!--      <div class="form-inputs">-->
            <!--        <v-text-field label="Repeat Password" type="text" id="password" name="password" v-model="input.password" placeholder="Repeat Password" />-->
            <!--      </div>-->
            <v-row>
              <v-col cols="4" class="d-flex child-flex">
                <div class="form-inputs">
                  <v-text-field label="Invitation Code" type="text" id="invitationCode" name="invitationCode" v-model="input.invitationCode" placeholder="Invitation Code" />
                </div>
              </v-col>
            </v-row>
            <v-btn type="button" v-on:click="register()">Register</v-btn>
            <p class="forgot-password text-right">
              Already have an account
              <router-link to="/login">Login Now</router-link>
            </p>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import axios from "axios";
import Home from "@/components/Home";
import Login from "@/components/Login";

export default {
  data() {
    return {
      input: {
        phoneNumber: "",
        password: ""
      }
    }
  },
  methods: {
    register() {
      if(this.input.username != "" && this.input.password != "") {
        // This should actually be an api call not a check against this.$parent.mockAccount
        const url = "http://localhost:8090/auth/register" //give suitable appi url
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
            this.goToLoginPage();
          }
        })
      } else {
        console.log("A Phone Number and password must be present");
      }
    },
    goToMainPage(){
      this.routeToPage('/home', Home);
    },
    goToLoginPage(){
      this.routeToPage('/login', Login);
    },
    routeToPage(path, component){
      this.$router.push({ path: path, component:component })
    }
  }

}
</script>