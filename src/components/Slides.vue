<template>
  <div class="slide">
    <Slide>
      <a id="home" href="#">
        <span>HOME</span>
      </a>
      <a id="home" href="#">
        <span>VERIFY</span>
      </a>
    </Slide>
  </div>
</template>

<style>
.bm-burger-button {
  margin-top: 22% !important;
}

.bm-burger-bars {
  background-color: #9e9e9e;
}

.line-style {
  height: 10%;
}

.bm-item-list > * > span {
  margin-left: 0px;
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
