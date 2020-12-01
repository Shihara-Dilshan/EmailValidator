<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="info">
      <b-navbar-brand href="#" id="logo">Email Validator</b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        

        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          
         <b-avatar id="badge" badge badge-variant="danger" src="https://avatars1.githubusercontent.com/u/61949881?s=460&u=093cb2d9dcd3f29f054c3143a7dd06569b928975&v=4"></b-avatar>

         
         
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
export default {
    name: "Navbar"
};
</script>

<style scoped>
   #badge {
      margin-right: 30px;
   }
   
   #logo {
      margin-left: 30px;
   }
</style>
