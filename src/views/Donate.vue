<template>
  <div id="app">
    <div
      class="background"
      :style="{
        backgroundImage: 'url(' + require('../assets/bg2.jpg') + ')',
      }"
    >
      <div class="overlay1">
        <b-container style="margin-top: 50px">
          <b-row>
            <b-col><img src="../assets/QR_Code.png" /></b-col>
            <b-col style="align-self: center"
              ><h5 style="color: white">
                THIS IS A NON-PROFITABLE PROJECT. PLEASE DONATE FOR US TO KEEP
                THIS PROJECT FUNCTIONING!
              </h5></b-col
            >
          </b-row>
        </b-container>
      </div>
    </div>
    <Header heading="CREATE YOUR PROOF" />
    <Slides />
  </div>
</template>

<script>
import Header from "@/components/Header.vue";
import Slides from "@/components/Slides.vue";

// import VueFileAgent from 'vue-file-agent';

export default {
  name: "Donate",
  data() {
    return {};
  },
  components: {
    Slides,
    Header,
  },
};
</script>

<style scoped>
.create {
  display: grid;
  align-content: center;
  padding-top: 130px;
  justify-items: center;
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.background {
  min-height: 100vh;
  background-size: 100% 100%;
}
.overlay1 {
  position: relative;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  background-color: #00000000;
  display: grid;
  align-items: center;
}

.contain {
  height: 100%;
  align-items: center;
  justify-content: center;
  color: white;
}
</style>
