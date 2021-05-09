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
            <b-col
              sm="6"
              class="animate__animated animate__fadeInLeft"
              style="animation-duration: 3s"
              ><img src="../assets/QR_Code.png" />
            </b-col>
            <b-col
              sm="6"
              class="animate__animated animate__fadeInRight"
              style="align-self: center; animation-duration: 3s"
              ><h5 style="color: white">
                THIS IS A NON-PROFITABLE ORGANISATION <br />
                PLEASE DONATE TO KEEP <br />THIS PROJECT RUNNING!
              </h5>
              <h5 style="color: white">
                <br />
                BITCOIN TESTNET ADDRESS :<br /><br />
                mn9skozk63Aw6VF8Sc6RSW6CVY2FYDv5g9
              </h5>
            </b-col>
          </b-row>
        </b-container>
      </div>
    </div>
    <Header heading="DONATE" />
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
