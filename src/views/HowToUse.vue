<template>
  <div id="app">
    <div
      class="background"
      :style="{
        backgroundImage: 'url(' + require('../assets/bg2.jpg') + ')',
      }"
    >
      <div class="overlay1">
        <div class="howtouse">
          <b-container>
            <h1>How to create your proof</h1>
            <b-row style="margin-top: 50px">
              <b-col sm="6">
                <img style="width: 100%" src="../assets/create1.png" />
              </b-col>
              <b-col sm="6" style="align-self: center"
                ><h6>
                  1. Choose the Files you want to create a proof for
                </h6></b-col
              >
            </b-row>
            <b-row class="mt-5">
              <b-col sm="6">
                <img style="width: 100%" src="../assets/create2.png" /> </b-col
              ><b-col sm="6" style="align-self: center"
                ><h6>
                  2. Fill in your Email ID to receive the transaction and proof
                  on your email (Optional)<br /><br />
                  Click on create your proof to proceed ahead
                </h6></b-col
              ></b-row
            >
            <b-row class="mt-5">
              <b-col sm="6">
                <img style="width: 100%" src="../assets/create3.png" /> </b-col
              ><b-col sm="6" style="align-self: center"
                ><h6>
                  3. Hola! Your proof is ready!

                  <br /><br />
                  You can save the proof as any file type of your choice : csv
                  or json <br /><br />
                  Alternatively, you can also copy the details <br /><br />
                  You can check the transaction id on the bitcoin blockchain
                  also

                  <br /><br />
                  If you see an error, wait for a couple of minutes and try
                  again to see it on bitcoin blockchain.
                </h6></b-col
              ></b-row
            >
          </b-container>
          <b-container class="mt-5">
            <h1>How to verify your proof</h1>
            <b-row style="margin-top: 50px">
              <b-col sm="6" style="align-self: center"
                ><h6>1. Choose the File that you want to verify</h6></b-col
              ><b-col sm="6">
                <img style="width: 100%" src="../assets/verify1.png" />
              </b-col>
            </b-row>
            <b-row class="mt-5">
              <b-col sm="6" style="align-self: center"
                ><h6>
                  2. Fill in the transaction id and the file path for that
                  respective file
                  <br /><br />
                  Click on verify to proceed ahead
                </h6></b-col
              ><b-col sm="6">
                <img style="width: 100%" src="../assets/verify2.png" /> </b-col
            ></b-row>
            <b-row class="mt-5">
              <b-col sm="6" style="align-self: center"
                ><h6>
                  3. If successful, the screen will display verification
                  successful otherwise verification failed
                </h6></b-col
              ><b-col sm="6">
                <img style="width: 100%" src="../assets/verify3.png" /> </b-col
            ></b-row>
          </b-container>
        </div>
      </div>
    </div>
    <Header heading="HOW TO USE" />
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
  height: 100%;
  background-color: #00000000;
  display: block;
  align-items: center;
}

.contain {
  height: 100%;
  align-items: center;
  justify-content: center;
  color: white;
}

.howtouse {
  padding-top: 25vh;
  color: white;
}
</style>
