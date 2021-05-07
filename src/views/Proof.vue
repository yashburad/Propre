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
          <!-- <div style="display: flex; justify-content: center"> -->
          <b-container>
            <b-row>
              <b-col
                ><b-button @click="redirect()" size="lg"
                  >CHECK IT ON BLOCKCHAIN</b-button
                ></b-col
              ></b-row
            >
            <b-row>
              <b-col>
                <b-button @click="save_json()" size="lg"
                  >SAVE YOUR PROOF AS JSON</b-button
                >
              </b-col>
              <b-col>
                <b-button @click="save_csv()" size="lg"
                  >SAVE YOUR PROOF AS CSV</b-button
                >
              </b-col>
            </b-row>
          </b-container>
          <!-- </div> -->
          <b-container class="mb-3"
            ><b-row class="d-flex">
              <b-col sm="3" class="p-0" style="align-self: center">
                <h5 style="margin: 0px 10px; text-transform: uppercase">
                  Transaction Number :
                </h5>
              </b-col>
              <b-col sm="8">
                <b-form-input
                  :value="this.dict['Transaction ID']"
                  readonly
                ></b-form-input>
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
                <b-modal
                  ref="my-modal"
                  :header-bg-variant="dark"
                  :header-text-variant="light"
                  :body-bg-variant="dark"
                  :body-text-variant="light"
                  :footer-bg-variant="dark"
                  :footer-text-variant="light"
                  :hide-header="true"
                  :ok-only="true"
                  :ok-variant="secondary"
                >
                  Copied</b-modal
                >
              </b-col>
            </b-row></b-container
          >

          <div
            class="path"
            v-for="(item, keys) in dict['Files Path']"
            :key="keys"
          >
            <Clipboard :dict="item" :filename="keys" />
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
      dark: "dark",
      light: "light",
      secondary: "secondary",
      dict: this.$route.params.dict,
      y: "a",
    };
  },
  components: {
    Slides,
    Header,
    Clipboard,
  },
  methods: {
    redirect: function () {
      let x =
        "https://www.blockchain.com/btc-testnet/tx/" +
        this.dict["Transaction ID"];
      window.open(x, "_blank");
    },
    save_json: function () {
      var FileSaver = require("file-saver");
      var blob = new Blob([JSON.stringify(this.dict, null, 4)], {
        type: "text/plain;charset=utf-8",
      });
      FileSaver.saveAs(blob, "transaction_details.json");
    },
    save_csv: function () {
      let csv = "Transaction ID,File Name,File Path\n";
      for (var keys in this.dict["Files Path"]) {
        csv +=
          this.dict["Transaction ID"] +
          "," +
          keys +
          "," +
          this.dict["Files Path"][keys] +
          "\n";
      }
      // console.log(csv);
      var FileSaver = require("file-saver");
      var blob = new Blob([csv], {
        type: "text/plain;charset=utf-8",
      });
      FileSaver.saveAs(blob, "transaction_details.csv");
    },
    doCopy: function () {
      this.$copyText(this.dict["Transaction ID"]).then(
        function (e) {
          console.log(e);
        }.then(this.$refs["my-modal"].show()),
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

.btn-secondary {
  background-color: transparent !important;
  color: #ffffff;
  margin-bottom: 20px;
}
</style>
