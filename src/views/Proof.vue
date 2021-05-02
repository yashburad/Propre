<template>
  <div id="app">
    <div
      class="background"
      :style="{
        backgroundImage: 'url(' + require('../assets/bg2.jpg') + ')',
      }"
    >
      <div class="overlay1">
        <div class="proof">
          <h2>Thank you for using Propre.com!</h2>
          <h3 class="mb-4" style="margin: 20px 0px">Proof Details</h3>
          <b-container class="mb-3"
            ><b-row class="d-flex">
              <b-col sm="3" class="p-0" style="align-self: center">
                <h5 style="margin: 0px 10px; text-transform: uppercase">
                  Transaction Number :
                </h5>
              </b-col>
              <b-col sm="8">
                <b-form-input :value="this.transaction" readonly></b-form-input>
              </b-col>
              <b-col style="text-align: left" sm="1">
                <svg
                  @click="doCopy"
                  v-bind:title="message"
                  xmlns="http://www.w3.org/2000/svg"
                  width="16"
                  height="16"
                  fill="currentColor"
                  class="bi bi-clipboard"
                  viewBox="0 0 16 16"
                >
                  <path
                    d="M4 1.5H3a2 2 0 0 0-2 2V14a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V3.5a2 2 0 0 0-2-2h-1v1h1a1 1 0 0 1 1 1V14a1 1 0 0 1-1 1H3a1 1 0 0 1-1-1V3.5a1 1 0 0 1 1-1h1v-1z"
                  />
                  <path
                    d="M9.5 1a.5.5 0 0 1 .5.5v1a.5.5 0 0 1-.5.5h-3a.5.5 0 0 1-.5-.5v-1a.5.5 0 0 1 .5-.5h3zm-3-1A1.5 1.5 0 0 0 5 1.5v1A1.5 1.5 0 0 0 6.5 4h3A1.5 1.5 0 0 0 11 2.5v-1A1.5 1.5 0 0 0 9.5 0h-3z"
                  />
                </svg>
              </b-col> </b-row
          ></b-container>

          <div class="path" v-for="keys in dict" :key="keys.fileName">
            <Clipboard :dict="keys" />
          </div>
        </div>
      </div>
    </div>
    <Header heading="PROOF" />

    <Slides />
  </div>
</template>

<script>
import Header from "@/components/Header.vue";
import Slides from "@/components/Slides.vue";
import Clipboard from "@/components/Clipboard.vue";

export default {
  name: "Home",
  data() {
    return {
      message: "Copy to the clipboard",
      transaction:
        "2db8334dec8121c455a8f0b17e2f79823d556e0205a9337490fb35a86db4f5ee",
      dict: [
        {
          fileName: "file_name",
          path:
            " 2db8334dec8121c455a8f0b17e2f79823d556e0205a9337490fb35a86db4f5ee,2db8334dec8121c455a8f0b17e2f79823d556e0205a9337490fb35a86db4f5ee",
        },
        {
          fileName: "file_namefile_name",
          path:
            "2db8334dec8121c455a8f0b17e2f79823d556e0205a9337490fb35a86db4f5ee,2db8334dec8121c455a8f0b17e2f79823d556e0205a9337490fb35a86db4f5ee",
        },
        {
          fileName: "file_namefile_namefile_name",
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
  methods: {
    doCopy: function () {
      this.$copyText(this.transaction).then(
        function (e) {
          alert("Copied");
          console.log(e);
        },
        function (e) {
          alert("Can not copy");
          console.log(e);
        }
      );
    },
  },
};
</script>

<style scoped>
.form-control {
  background: transparent;
  color: white;
  text-transform: uppercase;
}

input {
  overflow: hidden;
}

.path {
  text-align: left;
  display: flex;
  padding: 25px 0px;
}

.proof {
  color: white;
  padding-top: 25vh;
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
