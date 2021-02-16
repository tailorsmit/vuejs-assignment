<template>
  <div class="vue-tempalte">
    <form v-on:submit="sign_in">
      <h3>Sign In</h3>

      <div class="form-group">
        <label>Username</label>
        <input type="text" class="form-control form-control-lg" v-model="email"/>
      </div>

      <div class="form-group">
        <label>Password</label>
        <input type="password" class="form-control form-control-lg" v-model="password"/>
      </div>

      <button type="submit" class="btn btn-dark btn-lg btn-block">Sign In</button>

      <p class="forgot-password text-right mt-2 mb-4">
        <router-link to="/forgot-password">Forgot password ?</router-link>
      </p>
    </form>
  </div>
</template>

<script>
import axios from "axios"


export default {

  data() {
    return {
      email: '',
      password: '',
    }
  },
  methods: {
    async sign_in() {
      event.preventDefault();
      // POST request using axios with set headers
      if(this.email === '' || this.password==='') {
        if (this.email === '') alert("please enter username");
        if (this.password === '') alert("please enter password");
        return
      }
      const body = {
        username: this.email,
        password: this.password
      };
      console.log(body)
      const headers = {
        "content-type":"application/json"
      };
      await axios.post("http://localhost:8080/users/login", body, {headers})
          .then(response => {
            console.log(response);
            if (response.data === "SUCCESS") alert("signed in successfully");
            else alert("something went wrong!\n \ncheck credentials and try again!");

          })
    }
  }

}

</script>
