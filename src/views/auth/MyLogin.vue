<template>
  <div id="auth">
      <div id="nav">
        <router-link to="/login">Login</router-link> 
      </div>
  
      <p> Enter your username to start video chat </p>
      <p>Create an account through your CometChat dashboard or login with one of our test users (superhero1, superhero2)</p>
      <form v-on:submit.prevent="authLoginUser">
          <div class="form-group">
              <input name="username" id="username" class="form-control" placeholder="Enter your username" v-model="username"/>
          </div>
          <div class="form-group">
              <button type="submit" class="btn btn-success"> Login <span v-if="showSpinner" class="fa fa-spin fa-spinner"></span></button>
          </div>
      </form>
  </div>
</template>

<script>
import { CometChat } from "@cometchat-pro/chat";
export default {
  name: "login",
  data() {
    return {
      username: "",
      showSpinner: false
    };
  },
  methods: {
    authLoginUser() {
      var apiKey = 'e6287049934e453528184f0fe4a64dd1b78fccb4';
      console.log(apiKey, 'apikey')
      this.showSpinner = true;
      CometChat.login(this.username, apiKey).then(
        () => {
          this.showSpinner = false;
          this.$router.push({ name: "home" });
        },
        error => {
          this.showSpinner = false;
          console.log("Login failed with error:", error.code);
        }
      );
    }
  }
};
</script>