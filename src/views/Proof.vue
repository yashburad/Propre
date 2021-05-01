<template>
  <div id="app">
    <div
      class="background"
      :style="{
        backgroundImage: 'url(' + require('../assets/images.jpg') + ')',
      }"
    >
      <div class="overlay1">
        <Header heading="PROOF" />
        <div class="proof">
          <h2>Thank you for using Propre.com!</h2>
          <h3 style="margin-top: 20px">Proof Details</h3>

          <div style="text-align: -webkit-center">
            <h5 style="width: 80%; overflow-wrap: break-word; margin: 20px 0px">
              Transaction Number :
              2db8334dec8121c455a8f0b17e2f79823d556e0205a9337490fb35a86db4f5ee
            </h5>
          </div>
          <div class="path" v-for="keys in dict" :key="keys.fileName">
            <!-- <div style="padding: 20px 0px; display: contents"> -->
            <Clipboard :dict="keys" />
          </div>
        </div>
      </div>
    </div>
    <!-- <Clipboard /> -->

    <Slides />
  </div>
</template>

<script>
import Header from "@/components/Header.vue";
import Slides from "@/components/Slides.vue";
import Clipboard from "@/components/Clipboard.vue";
// import VueFileAgent from 'vue-file-agent';

export default {
  name: "Home",
  data() {
    return {
      message: "Copy to the clipboard",
      dict: [
        {
          fileName: "file_name",
          path:
            " 2db8334dec8121c455a8f0b17e2f79823d556e0205a9337490fb35a86db4f5ee,2db8334dec8121c455a8f0b17e2f79823d556e0205a9337490fb35a86db4f5ee",
        },
        {
          fileName: "file_name",
          path:
            "2db8334dec8121c455a8f0b17e2f79823d556e0205a9337490fb35a86db4f5ee,2db8334dec8121c455a8f0b17e2f79823d556e0205a9337490fb35a86db4f5ee",
        },
        {
          fileName: "file_name",
          path:
            "2db8334dec8121c455a8f0b17e2f79823d556e0205a9337490fb35a86db4f5ee,2db8334dec8121c455a8f0b17e2f79823d556e0205a9337490fb35a86db4f5ee",
        },
        {
          fileName: "file_name",
          path:
            "2db8334dec8121c455a8f0b17e2f79823d556e0205a9337490fb35a86db4f5ee,2db8334dec8121c455a8f0b17e2f79823d556e0205a9337490fb35a86db4f5ee",
        },
      ],
      y: "a",
    };
  },
  components: {
    Slides,
    Header,
    Clipboard,
  },
  methods: {},
};
</script>

<style>
.path {
  width: 80%;
  margin-left: 20vh;
  text-align: left;
  display: flex;
  padding: 25px 0px;
  /* overflow-wrap: break-word; */
}
.proof {
  color: white;
  padding-top: 30px;
  font-weight: 100;
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
