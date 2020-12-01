<template>
  <div id="app">
    <Navbar />
    <div id="jambo">
      <b-jumbotron>

      <h2 id="heading"><b-badge>Email Validator with ZeroBounce API</b-badge></h2>
            <h3>Instructions</h3>
       <b-list-group>
  <b-list-group-item class="d-flex justify-content-between align-items-center">
    Enter an email
    <b-badge variant="primary" pill>1</b-badge>
  </b-list-group-item>

  <b-list-group-item class="d-flex justify-content-between align-items-center">
    Click on check
    <b-badge variant="primary" pill>2</b-badge>
  </b-list-group-item>

  <b-list-group-item class="d-flex justify-content-between align-items-center">
     View the results
    <b-badge variant="primary" pill>3</b-badge>
  </b-list-group-item>
</b-list-group>
          <br />
        <div id="inputfeild">
          <b-form-input
            v-model="input_email"
            v-on:keyup.enter="validateWithZeroBouce"
            placeholder="Enter an email"
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
        <b-progress v-else-if="valid === 'wait' " :value="value" :max="max" show-progress animated></b-progress>
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
      api_key: "b892d2302e654860a079c864a54d184a",
        value: 0,
        max: 100,
        intervel: 0,
    };
  },
  methods: {
  
    randomValue() {
        
        this.intervel = setInterval( () => {
            if(this.value < 100){
                this.value = this.value +5;
            }
        },500); 
        
      },
    async validateWithZeroBouce() {
      this.randomValue();
      this.valid = "wait";
      const validateCall = await fetch(
        `https://api.zerobounce.net/v1/validatewithip?apikey=${this.api_key}&email=${this.input_email}&ipAddress=156.124.12.145`
      );
      const result = await validateCall.json();

      if(result.status === 'Invalid'){
          this.valid = false;
          this.value = 0;
          clearInterval(this.intervel);
      }else if(result.status === 'Valid'){
          this.valid = true;
          this.value = 0;
          clearInterval(this.intervel);
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

#inputfeild {
     margin-top: 20px;
}

#heading {
    margin-bottom: 20px;
}

#btn {
  width: 100%;
  margin-top: 2%;
  margin-bottom: 2%;
}

ul,
p {
  margin-top: 1%;
  list-style: none;
}

#jambo {
  padding: 0%;
  text-align: center;
}
</style>
