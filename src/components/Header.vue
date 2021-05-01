<template>
  <div class="header">
    <b-navbar variant="black" type="dark">
      <h2 style="color: #9e9e9e; font-weight: 100; margin-bottom: 0px">
        {{ this.heading }}
      </h2>
      <b-navbar-nav class="ml-auto" variant="black" type="dark">
        <!-- <b-button variant="outline-light">Fork on GitHub</b-button> -->
      </b-navbar-nav>
      <b-navbar-brand href="/" style="font-size: 30px; letter-spacing: 10px"
        ><img style="height: 15vh" src="@/assets/logo4-min.png"
      /></b-navbar-brand>
    </b-navbar>
  </div>
</template>

<style scoped>
.header {
  padding: 0px 55px;
  border-bottom: 1px solid white;
  /* position: absolute;
  top: 0px;
  width: 100%; */
}
</style>

<script>
// @ is an alias to /src
// import Logo from "@/assets/ep-logo.png";

export default {
  props: {
    heading: String,
  },
};
</script>
