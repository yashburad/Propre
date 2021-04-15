<template>
  <div id="app">
    <div
      class="background"
      :style="{
        backgroundImage: 'url(' + require('../assets/images.jpg') + ')',
      }"
    >
      <div class="overlay1">
        <Header />

        <div class="create">
          <!-- <textarea rows="10" v-model="text"></textarea> -->
          <!-- <br />
          <text-reader @load="text = $event"></text-reader> -->
          <h2>{{ text }}</h2>
          <VueFileAgent
            :multiple="true"
            :maxFiles="20"
            :deletable="true"
            class="animate__animated animate__fadeInDown"
            style="animation-duration: 5s"
            :uploadUrl="uploadUrl"
            v-model="fileRecords"
            @select="filesSelected($event)"
            @delete="fileDeleted($event)"
            @beforedelete="onBeforeDelete($event)"
          ></VueFileAgent>
          <div style="padding-top: 40px">
            <b-button size="lg" @click="computehash()"
              >Create Your Proof</b-button
            >
          </div>
        </div>
      </div>
    </div>

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
      // fileRecords: [],
      dict1: new Object(),
      dict: new Object(),
      text: "",
      file: "",
      fileRecords: [],
      uploadHeaders: { "X-Test-Header": "vue-file-agent" },
      fileRecordsForUpload: [],
    };
  },
  components: {
    Slides,
    Header,
    // TextReader,
    // VueFileAgent
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
      for (var member in this.dict) delete this.dict[member];
      var i;
      for (i = 0; i < this.fileRecordsForUpload.length; i++) {
        // this.text = i;
        this.file = this.fileRecordsForUpload[i];
        this.hash(this.file);
        // this.hash(i);
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
    fileDeleted: function (fileRecord) {
      var i = this.fileRecordsForUpload.indexOf(fileRecord);
      if (i !== -1) {
        this.fileRecordsForUpload.splice(i, 1);
      } else {
        this.deleteUploadedFile(fileRecord);
      }
    },
    onBeforeDelete: function (fileRecord) {
      var i = this.fileRecordsForUpload.indexOf(fileRecord);
      if (i !== -1) {
        // queued file, not yet uploaded. Just remove from the arrays
        this.fileRecordsForUpload.splice(i, 1);
        var k = this.fileRecords.indexOf(fileRecord);
        if (k !== -1) this.fileRecords.splice(k, 1);
      } else {
        if (confirm("Are you sure you want to delete?")) {
          this.$refs.vueFileAgent.deleteFileRecord(fileRecord); // will trigger 'delete' event
        }
      }
    },
  },
};
</script>

<style>
.create {
  height: calc(100vh - 157px);
  overflow: scroll;
  display: grid;
  align-content: center;
  padding-top: 30px;
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
  height: 100%;
  background-color: #00000000;
  /* opacity: 0.5; */
  display: block;
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
