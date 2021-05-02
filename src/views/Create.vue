<template>
  <div id="app">
    <div
      class="background"
      :style="{
        backgroundImage: 'url(' + require('../assets/bg1.jpg') + ')',
      }"
    >
      <div class="overlay1">
        <div class="create">
          <VueFileAgent
            :theme="'list'"
            :multiple="true"
            :maxFiles="20"
            :deletable="true"
            class="animate__animated animate__fadeInDown"
            style="
              animation-duration: 5s;
              width: 70%;
              overflow: scroll;
              max-height: 40vh;
            "
            :uploadUrl="uploadUrl"
            v-model="fileRecords"
            @select="filesSelected($event)"
            @beforedelete="onBeforeDelete($event)"
          ></VueFileAgent>
          <div style="padding-top: 40px">
            <router-link to="/proof">
              <b-button size="lg">Create Your Proof</b-button>
            </router-link>
            <!-- <b-button size="lg" @click="computehash()">
              <router-link style="color: white" to="/proof">
                Create Your Proof
              </router-link></b-button
            > -->
          </div>
        </div>
      </div>
    </div>
    <Header heading="CREATE YOUR PROOF" />
    <Slides />
  </div>
</template>

<script>
import Header from "@/components/Header.vue";
import Slides from "@/components/Slides.vue";

// import VueFileAgent from 'vue-file-agent';

export default {
  name: "Home",
  data() {
    return {
      dict: {},
      text: "",
      file: "",
      text1: "",
      fileRecords: [],
      uploadHeaders: { "X-Test-Header": "vue-file-agent" },
      fileRecordsForUpload: [],
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
      if (this.text1 === "A") {
        this.text1 = "B";
      } else {
        this.text1 = "A";
      }
      var i;
      for (i = 0; i < this.fileRecords.length; i++) {
        this.file = this.fileRecords[i];
        this.hash(this.file);
      }
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
.create {
  /* height: calc(100vh - 157px); */
  /* overflow: scroll; */
  display: grid;
  align-content: center;
  padding-top: 130px;
  /* text-align: -webkit-center; */
  justify-items: center;
}

.btn-secondary {
  background-color: transparent !important;
  color: #ffffff;
  border-color: white;
  /* margin-top: 20px; */
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /* margin-top: 60px; */
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
  /* opacity: 0.5; */
  display: grid;
  align-items: center;
  /* animation: mymove 3s;
  animation-fill-mode: forwards; */
  /* animation-iteration-count: 1; */
}

@keyframes mymove {
  from {
    background-color: #00000000;
  }
  to {
    background-color: #000000c4;
  }
}

.theme-list::-webkit-scrollbar {
  display: none;
}

.contain {
  height: 100%;
  align-items: center;
  justify-content: center;
  color: white;
}

.theme-undefined {
  width: 70%;
  justify-self: center;
  overflow: scroll;
}
</style>
