<template>
  <div class="header">
    <b-navbar variant="black" type="dark">
      <router-link to="/">
        <b-navbar-brand href="/" style="font-size: 30px; letter-spacing: 10px"
          ><img style="height: 100px" src="@/assets/logo2.png"
        /></b-navbar-brand>
      </router-link>

      <!-- <b-navbar-nav class="ml-auto" variant="black" type="dark">
        <b-button variant="outline-light">Fork on GitHub</b-button>
      </b-navbar-nav> -->
    </b-navbar>
  </div>
</template>

<style scoped>
.header {
  /* padding: 15px 45px; */
  border-bottom: 1px solid white;
  /* position: absolute;
  top: 0px;
  width: 100%; */
}
</style>

<script>
// @ is an alias to /src
// import Logo from "@/assets/ep-logo.png";

export default {};
</script>
