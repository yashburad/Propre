<template>
  <div id="app">
    <div
      class="background"
      :style="{
        backgroundImage: 'url(' + require('../assets/bg2.jpg') + ')',
      }"
    >
      <div class="overlay1">
        <div
          class="animate__animated animate__fadeInDown verify"
          style="padding-top: 5%; animation-duration: 4s"
        >
          <!-- <h1>VERIFICATION</h1> -->
          <div style="display: flex; justify-content: center">
            <div class="verify-data">
              <VueFileAgent
                :theme="'list'"
                :maxFiles="1"
                :deletable="true"
                v-model="fileRecords"
                @select="filesSelected($event)"
                @beforedelete="onBeforeDelete($event)"
              ></VueFileAgent>
              <div style="display: flex; margin-top: 50px; align-items: center">
                <b-form-input
                  placeholder="ENTER TRANSACTION ID"
                  v-model="transactionId"
                ></b-form-input>
              </div>
              <div style="display: flex; margin-top: 50px; align-items: center">
                <!-- <h3>File Path:</h3> -->
                <b-form-input
                  placeholder="ENTER FILE PATH"
                  v-model="filePath"
                ></b-form-input>
              </div>
              <b-button size="lg" @click="create()"> VERIFY </b-button>
            </div>
          </div>
        </div>
      </div>
    </div>
    <b-modal
      title="Result"
      :header-bg-variant="dark"
      :header-text-variant="light"
      :body-bg-variant="dark"
      :body-text-variant="light"
      :footer-bg-variant="dark"
      :footer-text-variant="light"
      v-model="showModal"
    >
      Verification {{ this.verify }}</b-modal
    >
    <!-- <Clipboard /> -->
    <Header heading="VERIFY" />

    <Slides />
  </div>
</template>

<script>
import Header from "@/components/Header.vue";
import Slides from "@/components/Slides.vue";
// import VueFileAgent from 'vue-file-agent';

export default {
  name: "Verify",
  data() {
    return {
      dark: "dark",
      light: "light",
      dict: {},
      text: "",
      file: "",
      fileRecords: [],
      fileRecordsForUpload: [],
      transactionId: "",
      filePath: "",
      showModal: false,
      verify: null,
    };
  },
  updated: function () {
    this.computehash();
  },
  components: {
    Slides,
    Header,
  },
  methods: {
    create: function () {
      if (
        this.transactionId == "" ||
        this.filePath == "" ||
        this.fileRecordsForUpload.length == 0
      ) {
        alert("Please fill all the details");
        return;
      }
      let hash;
      var key;
      for (key in this.dict) {
        console.log(key);
        hash = this.dict[key];
      }
      let x =
        "https://propre-api.herokuapp.com/propre-api/verify?txid=" +
        this.transactionId +
        "&path=" +
        this.filePath +
        "&hash=" +
        hash;
      console.log(x);
      fetch(x)
        .then((response) => response.json())
        .then(
          (result) =>
            (this.verify = result["verify"] == false ? "Failed" : "Succeeded")
        )
        .then((this.showModal = true))
        .catch((error) => console.log("error", error));
    },
    hash: function (x) {
      var SHA256 = require("crypto-js/sha256");
      const reader = new FileReader();
      reader.readAsText(x.file, "UTF-8");
      reader.onload = (evt) => {
        this.text = SHA256(evt.target.result).toString();
        this.dict[x.file.name] = this.text;
      };
    },
    computehash: function () {
      this.file = this.fileRecords[0];
      // console.log(this.file.file.name);
      this.hash(this.file);
    },
    filesSelected: function (fileRecordsNewlySelected) {
      var validFileRecords = fileRecordsNewlySelected.filter(
        (fileRecord) => !fileRecord.error
      );
      this.fileRecordsForUpload = this.fileRecordsForUpload.concat(
        validFileRecords
      );
    },
    onBeforeDelete: function (fileRecord) {
      var i = this.fileRecordsForUpload.indexOf(fileRecord);
      var name = this.fileRecordsForUpload[i].file.name;
      delete this.dict[name];
      if (i !== -1) {
        this.fileRecordsForUpload.splice(i, 1);
        var k = this.fileRecords.indexOf(fileRecord);
        if (k !== -1) this.fileRecords.splice(k, 1);
      } else {
        if (confirm("Are you sure you want to delete?")) {
          this.$refs.vueFileAgent.deleteFileRecord(fileRecord);
        }
      }
    },
  },
};
</script>

<style scoped>
/* ::placeholder {
  color: white;
  opacity: 1; 
}

:-ms-input-placeholder {
  color: white;
}

::-ms-input-placeholder {
  color: white;
} */

.modal-header {
  border-bottom: 1px solid #3c3e40 !important;
}

.form-control {
  border: none;
  width: 100%;
  background: white;
  margin-left: auto;
}

.btn-secondary {
  background-color: transparent !important;
  color: #ffffff;
  /* border-color: white; */
  margin-top: 50px;
}

.btn-secondary:hover {
  border-color: #545b62;
}

.verify-data {
  width: 70%;
  margin-top: 30px;
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

h5,
h1 {
  margin-top: 30px;
  margin-bottom: 0px;
  color: white;
}

h3 {
  color: #aaaaaa;
  margin-bottom: 0px;
}
</style>
