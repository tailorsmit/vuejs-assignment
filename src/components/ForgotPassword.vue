<template>
    <div class="vue-tempalte">
        <form v-on:submit="submit">
            <h3>Forgot Password</h3>

            <div class="form-group">
                <label>Username</label>
                <input type="text" class="form-control form-control-lg" v-model="email"/>
            </div>

            <div class="form-group">
              <label>Otp</label>
              <input type="number" class="form-control form-control-lg" v-model="otp"/>
            </div>

            <div class="form-group">
              <label>New Password</label>
              <input type="password" class="form-control form-control-lg" v-model="password"/>
            </div>

            <button type="submit" class="btn btn-dark btn-lg btn-block">Reset password</button>
        </form>
    </div>
</template>

<script>
    import axios from "axios";

    export default {
        data() {
            return {
              email: '',
              otp: Number ,
              password:''
            }
        },
      methods :{
        async submit() {
          event.preventDefault();
          if (!this.email || !this.password || !this.otp) {
            if (!this.email) alert("enter your email");
            if (!this.password) alert("enter new password");
            if (!this.otp) alert("please enter otp");
            return
          }

          const body = {
            username: this.email,
            password: this.password,
            otp: this.otp
          };
          console.log(body)
          const headers = {
            "content-type": "application/json"
          };
          await axios.post("http://localhost:8080/users/forgot-password", body, {headers})
              .then(response => {
                console.log(response);
                if (response.data === "SUCCESS") alert("password reseted successfully");
                else if(response.data === "FAILURE") alert("check username or Otp and try again");
              })
        }
      }
    }
</script>
