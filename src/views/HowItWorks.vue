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
          <b-row style="margin: 60px 0px; padding-bottom: 50px">
            <b-col>
              <iframe
                src="https://drive.google.com/file/d/1jr0hCHAZpGdYT4lWgfu8sxouE-w-wLvO/preview"
                width="700px"
                height="800px"
              ></iframe>
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
