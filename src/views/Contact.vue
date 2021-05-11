<template>
  <div id="app">
    <div
      class="background"
      :style="{
        backgroundImage: 'url(' + require('../assets/bg2.jpg') + ')',
      }"
    >
      <div class="overlay1">
        <div class="contactus">
          <h2>We would love to hear from you!</h2>
          <b-container>
            <b-row class="mt-5 mb-5">
              <b-col>
                <b-form-input placeholder="FIRST NAME"></b-form-input> </b-col
              ><b-col>
                <b-form-input placeholder="LAST NAME"></b-form-input>
              </b-col>
            </b-row>
            <b-row class="mt-5 mb-5">
              <b-col>
                <b-form-input placeholder="EMAIL ID"></b-form-input> </b-col
              ><b-col>
                <b-form-input placeholder="PHONE NUMBER"></b-form-input>
              </b-col>
            </b-row>
            <b-row class="mt-5 mb-5">
              <b-col>
                <b-form-input
                  style="height: 15vh"
                  size="lg"
                  placeholder="FEEDBACK"
                ></b-form-input>
              </b-col>
            </b-row>
            <b-button size="lg"> SUBMIT </b-button>
          </b-container>
        </div>
      </div>
    </div>
    <!-- <Clipboard /> -->
    <Header heading="CONTACT US" />

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
a {
  color: white;
}

.contactus {
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

.form-control {
  border: none;
  background: white;
}

.btn-secondary {
  background-color: transparent !important;
  color: #ffffff;
  /* border-color: white; */
  padding: 0.5rem 5rem;
}

.btn-secondary:hover {
  border-color: #545b62;
}
</style>
