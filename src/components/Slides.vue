<template>
  <div class="slide">
    <Slide>
      <router-link to="/">
        <span>HOME</span>
      </router-link>

      <router-link to="/proof">
        <span>CREATE YOUR PROOF</span>
      </router-link>
      <router-link to="/verify">
        <span>VERIFY</span>
      </router-link>
      <a id="home" href="#">
        <span>ABOUT US</span>
      </a>
      <!-- <a id="home" href="#">
        <span>VERIFY</span>
      </a> -->
    </Slide>
  </div>
</template>

<style>
.bm-burger-button {
  margin-top: 45vh !important;
}

.bm-burger-bars {
  background-color: #9e9e9e;
}

.bm-menu {
  /* width: 300px; */
  /* display: grid; */
  /* align-content: center; */
}

.line-style {
  height: 10%;
}

.bm-item-list > * > span {
  margin-left: 0px;
  color: #fff;
  font-weight: 500;
  letter-spacing: 5px;
  font-size: unset;
}

.bm-item-list > * {
  justify-content: center;
}

.bm-item-list {
  margin-left: 0px;
}
</style>

<script>
// @ is an alias to /src
import { Slide } from "vue-burger-menu"; // import the CSS transitions you wish to use, in this case we are using `Slide`

export default {
  name: "Home",
  components: {
    Slide,
  },
};
</script>
