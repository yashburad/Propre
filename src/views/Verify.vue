<template>
  <div id="app">
    <div
      class="background"
      :style="{
        backgroundImage: 'url(' + require('../assets/bg2.jpg') + ')',
      }"
    >
      <div class="overlay1">
        <div class="verify" style="padding-top: 5%">
          <h1>VERIFICATION</h1>
          <div style="text-align: -webkit-center">
            <div class="verify-data">
              <VueFileAgent
                :theme="'list'"
                :maxFiles="1"
                :deletable="true"
                class="animate__animated animate__fadeInDown"
                style="animation-duration: 2s"
                :uploadUrl="uploadUrl"
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
              <b-button size="lg" @click="computehash()"> VERIFY </b-button>
            </div>
          </div>
        </div>
      </div>
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
    };
  },
  components: {
    Slides,
    Header,
  },
  methods: {
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
