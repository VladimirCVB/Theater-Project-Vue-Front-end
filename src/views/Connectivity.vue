<template>
  <div class="about flex items-center justify-center h-screen">
    <Connection v-on:login="login" v-on:registration="registration"/>
  </div>
</template>

<script>

import Connection from '../components/connectivity/Connection';
import axios from 'axios';

export default {
  name: "Connectivity",
  components: {
    Connection
  },
  methods: {
    checkError(error){
      if(error == 401){
        alert("Wrong credentials. Please try again.");
      }
      else {
        alert("Server error, please try again later.");
      }
    },

    login(user){

      const {email, password} = user;
      var params = new URLSearchParams();

      params.append('login', email);
      params.append('password', password);

      axios.post('http://localhost:9090/theater/users/login', params)
            .then(function(response) {
              
              //Set token expiration date
              let d = new Date();
              d.setTime(d.getTime() + 1 * 24 * 60 * 60 * 1000);
              let expires = "expires=" + d.toUTCString();

              //Set token in session storage
              document.cookie = "Token=" + response.data + ";" + expires + ";path=/";

              //Go to home after log in
              window.location.href = "/";
            }).catch(err => this.checkError(err.response.status));
    },

    registration(userRegistration){

      const {email, name, password} = userRegistration;
      var params = new URLSearchParams();

      params.append('email', email);
      params.append('name', name);
      params.append('password', password);

      axios.post('http://localhost:9090/theater/users/create', params)
            .then(alert("Successful registration! You can log in now."))
            .catch(err => alert("User with the same email address already exists. " + err));
    }
  }
}
</script>
