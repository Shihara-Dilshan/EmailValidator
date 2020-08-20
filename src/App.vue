<template>
  <div id="app">
    <Navbar />
    <div id="jambo">
      <b-jumbotron lead="Email Validator with Vue.js">
        <div>
          <b-form-input
            v-model="input_email"
            v-on:keyup.enter="validateWithZeroBouce"
            placeholder="Enter your name"
          ></b-form-input>
        </div>
        <b-button
          id="btn"
          variant="info"
          href="#"
          v-bind:disabled="input_email.length<=0"
          v-on:click="validateWithZeroBouce"
        >Check</b-button>
        <ul v-if="valid === true">
          <p>Email is valid</p>
          <li>account : {{valid_details.account}}</li>
          <li>address : {{valid_details.address}}</li>
          <li>domain : {{valid_details.domain}}</li>
          <li>status : {{valid_details.status}}</li>

        </ul>
        <p v-else-if="valid === false">Email is not valid</p>
        <p v-else-if="valid === 'wait' ">Please wait</p>
        <p v-else></p>
      </b-jumbotron>
    </div>
  </div>
</template>

<script>
import Navbar from "./Navbar.vue";

export default {
  name: "App",
  data() {
    return {
      input_email: "",
      valid: "",
      valid_details:{
        account: "",
        address: "",
        domain: "",
        status: "",
      },
      api_key: "b892d2302e654860a079c864a54d184a"
    };
  },
  methods: {
    async validateWithZeroBouce() {
      this.valid = "wait";
      const validateCall = await fetch(
        `https://api.zerobounce.net/v1/validatewithip?apikey=${this.api_key}&email=${this.input_email}&ipAddress=156.124.12.145`
      );
      const result = await validateCall.json();

      if(result.status === 'Invalid'){
          this.valid = false;
      }else if(result.status === 'Valid'){
          this.valid = true;
          this.valid_details.account = result.account;
          this.valid_details.address = result.address;
          this.valid_details.domain = result.domain;
          this.valid_details.status = result.status;
      }

      console.log(result);
    }
  },
  components: {
    Navbar
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}

#btn {
  width: 100%;
  margin-top: 2%;
}

ul,
p {
  margin-top: 1%;
  list-style: none;
}

#jambo {
  padding: 2%;
  text-align: center;
}
</style>
