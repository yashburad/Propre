<template>
  <div id="app">
    <div
      class="background"
      :style="{
        backgroundImage: 'url(' + require('../assets/bg2.jpg') + ')',
      }"
    >
      <div class="overlay1">
        <div class="aboutus">
          <h1>About the Project</h1>
          <b-container style="padding: 20px 0px">
            <b-row>
              <p>
                Proof of existence (Link) like application with the added
                functionality of adding more data per transaction (with the help
                of a Merkle tree). A service to anonymously and securely store
                an online distributed proof of existence for any document. Your
                documents are NOT stored in our database or in the bitcoin
                blockchain, so you don't have to worry about your data being
                accessed by others.
              </p>
            </b-row>
          </b-container>
          <h1>Founders</h1>
          <b-container style="margin-top: 50px">
            <b-row
              class="animate__animated animate__fadeInUp"
              style="animation-duration: 2s"
            >
              <b-col class="images">
                <img src="../assets/yash.jpg" />
                <h2>Yash Burad</h2>
              </b-col>
              <b-col class="images">
                <img src="../assets/yvj.jpg" />
                <h2>Yashvardhan Jain</h2>
              </b-col>
            </b-row>
          </b-container>
        </div>
      </div>
    </div>
    <!-- <Clipboard /> -->
    <Header heading="ABOUT US" />

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
};
</script>

<style scoped>
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
