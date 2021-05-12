<template>
  <div id="app">
    <div
      class="background"
      :style="{
        backgroundImage: 'url(' + require('../assets/bg2.jpg') + ')',
      }"
    >
      <div class="overlay1">
        <div class="aboutus"></div>
        <b-container>
          <h1 style="color: white">HOW DOES IT WORK</h1>
          <b-row>
            <b-col>
              <p style="color: white; text-align: justify; margin-top: 30px">
                Suppose a user wants to upload four files to the network. He
                uploads the files on PROPRE.com.The backend computes the hash of
                each file and merges it with the hashes of the other files.The
                figure below illustrates how this will be done.

                <br /><br />
                The user will receive the Transaction ID along with the
                following data for each file i:•Path Hash, linking the hash of
                File i to the hash data in the transactionTh transaction uses
                OP_RETURN to save the final hash data in the transaction on the
                network.This final hash data comprises of the hashes of all
                files together
              </p>
            </b-col>
          </b-row>
        </b-container>
      </div>
    </div>
    <!-- <Clipboard /> -->
    <Header heading="HOW DOES IT WORK" />

    <Slides />
  </div>
</template>

<script>
import Header from "@/components/Header.vue";
import Slides from "@/components/Slides.vue";

export default {
  name: "Home",
  data() {
    return {};
  },
  components: {
    Slides,
    Header,
  },
  methods: {},
  mounted() {
    window.scrollTo(0, 0);
  },
};
</script>

<style scoped>
a {
  color: white;
}

.images h2 {
  margin-top: 20px;
}

.about-data {
  display: flex;
  justify-content: center;
}

.aboutus img {
  height: 60vh;
  margin: 0px 40px;
  filter: grayscale(1);
}

.aboutus {
  padding-top: 25vh;
  color: white;
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
h5 {
  margin-bottom: 0px;
}
</style>
