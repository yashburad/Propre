<template>
  <div id="app">
    <div
      class="background"
      :style="{
        backgroundImage: 'url(' + require('../assets/images.jpg') + ')',
      }"
    >
      <div class="overlay1">
        <Header heading="VERIFY" />
      </div>
    </div>
    <!-- <Clipboard /> -->

    <Slides />
  </div>
</template>

<script>
import Header from "@/components/Header.vue";
import Slides from "@/components/Slides.vue";
// import VueFileAgent from 'vue-file-agent';

export default {
  name: "Verify",
  data() {
    return {};
  },
  components: {
    Slides,
    Header,
  },
  methods: {},
};
</script>

<style>
.background {
  min-height: 100vh;
  background-size: 100% 100%;
}
.overlay1 {
  position: relative;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: #00000000;
  display: block;
  align-items: center;
}
h5 {
  margin-bottom: 0px;
}
</style>
