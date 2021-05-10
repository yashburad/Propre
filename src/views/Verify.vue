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
          style="padding-top: 5%; animation-duration: 3s"
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
              <div
                style="
                  display: flex;
                  margin-top: 50px;
                  align-items: center;
                  justify-content: center;
                "
              >
                <b-form-input
                  style="width: 90%"
                  placeholder="ENTER TRANSACTION ID"
                  v-model="transactionId"
                ></b-form-input>
              </div>
              <div
                style="
                  display: flex;
                  margin-top: 50px;
                  align-items: center;
                  justify-content: center;
                "
              >
                <!-- <h3>File Path:</h3> -->
                <b-form-input
                  style="width: 80%"
                  placeholder="ENTER FILE PATH"
                  v-model="filePath"
                ></b-form-input>
              </div>
              <b-button size="lg" @click="create()"> VERIFY </b-button>
              <div style="display: flex; justify-content: center">
                <h4 class="error" v-show="this.bool">
                  PLEASE FILL ALL THE DETAILS
                </h4>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div v-show="this.loader" class="loader">
      <b-spinner
        style="width: 5rem; height: 5rem; color: white"
        label="Spinning"
      ></b-spinner>
    </div>
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
      dict: {},
      text: "",
      file: "",
      fileRecords: [],
      fileRecordsForUpload: [],
      transactionId: "",
      filePath: "",
      verify: null,
      bool: false,
      loader: false,
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
      if (this.transactionId == "" || this.fileRecordsForUpload.length == 0) {
        this.bool = true;
        return;
      }
      this.loader = true;
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
        .then((result) =>
          this.$router.push({
            name: "Result",
            params: { proof: result },
          })
        )
        .then()
        .catch((error) => {
          console.log("error", error);
          this.loader = false;
        });
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
.loader {
  position: fixed;
  top: 0px;
  width: 100%;
  height: 100%;
  background: rgb(0 0 0 / 60%);
  display: grid;
  place-content: center;
}
.error {
  animation: shake 0.82s cubic-bezier(0.36, 0.07, 0.19, 0.97) both;
  transform: translate3d(0, 0, 0);
  backface-visibility: hidden;
  perspective: 1000px;
  position: absolute;
  margin-top: 30px;
  color: #9aa0a8;
}

@keyframes shake {
  10%,
  90% {
    transform: translate3d(-1px, 0, 0);
  }

  20%,
  80% {
    transform: translate3d(2px, 0, 0);
  }

  30%,
  50%,
  70% {
    transform: translate3d(-4px, 0, 0);
  }

  40%,
  60% {
    transform: translate3d(4px, 0, 0);
  }
}

.modal-header {
  border-bottom: 1px solid #3c3e40 !important;
}

.form-control {
  border: none;
  background: white;
}

.btn-secondary {
  background-color: transparent !important;
  color: #ffffff;
  /* border-color: white; */
  margin-top: 50px;
  padding: 0.5rem 5rem;
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
