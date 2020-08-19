<template>
  <div id="app">
    <Navbar />
    <div id="jambo">
      <b-jumbotron lead="Email Validator with Vue.js">
        <div>
          <b-form-input v-model="text" placeholder="Enter your name"></b-form-input>
        </div>
        <b-button id="btn" variant="info" href="#">Check</b-button>
      </b-jumbotron>
    </div>
  </div>
</template>

<script>
import Navbar from "./Navbar.vue";

export default {
  name: "App",
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

#jambo {
  padding: 2%;
  text-align: center;
}
</style>
