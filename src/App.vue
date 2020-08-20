<template>
  <div id="app">
    <Navbar />
    <div id="jambo">
      <b-jumbotron lead="Email Validator with Vue.js">
        <div>
          <b-form-input
            v-model="input_email"
            v-on:keyup.enter="validate"
            placeholder="Enter your name"
          ></b-form-input>
        </div>
        <b-button
          id="btn"
          variant="info"
          href="#"
          v-bind:disabled="input_email.length<=0"
          v-on:click="validate"
        >Check</b-button>
        <p v-if="valid === true">Email is valid</p>
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
      api_key: "e0454de7a4161b8f149a90a4cb0461c25ecd959b",
      api_key2: "b892d2302e654860a079c864a54d184a"
    };
  },
  methods: {
    async validate() {
      this.valid = "wait";
      const validateCall = await fetch(
        `https://api.hunter.io/v2/email-verifier?email=${this.input_email}&api_key=${this.api_key}`
      );
      const result = await validateCall.json();

      result.data === undefined
        ? (this.valid = false)
        : result.data.result === "undeliverable"
        ? (this.valid = false)
        : (this.valid = true);
    },
    async validateWithZeroBouce() {
      this.valid = "wait";
      const validateCall = await fetch(
        `https://api.zerobounce.net/v1/validatewithip?apikey=b892d2302e654860a079c864a54d184a&email=valid@eddxample.com&ipAddress=156.124.12.145`
      );
      const result = await validateCall.json();
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
