<template>
  <div class="vue-tempalte">
    <form v-on:submit="sign_up">
      <h3 >Sign Up</h3>

      <div class="form-group">
        <label>Username</label>
        <input type="text" class="form-control form-control-lg" v-model="email"/>
      </div>

      <div class="form-group">
        <label>Password</label>
        <input type="password" class="form-control form-control-lg" v-model="password"/>
      </div>

      <button type="submit" class="btn btn-dark btn-lg btn-block">Sign Up</button>

      <p class="forgot-password text-right">
        Already registered
        <router-link :to="{name: 'login'}">sign in?</router-link>
      </p>
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      email: '',
      password: '',
    }
  },
  methods: {
    async sign_up() {
      event.preventDefault();
      // POST request using axios with set headers
      if (this.email === '') alert("please enter username");
      if (this.password === '') alert("please enter password");
      const body = {
        username: this.email,
        password: this.password
      };
      console.log(body)
      const headers = {};
      await axios.post("http://localhost:8080/users/register", body, {headers})
          .then(response => {
            console.log(response);
            if (response.data === "SUCCESS") alert("user created");
            else if(response.data === "USER_ALREADY_EXISTS") alert("user already exist");
          }).catch(error => console.log(error));
    }
  }
}

</script>
