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
          class="create animate__animated animate__fadeInDown"
          style="animation-duration: 3s"
        >
          <VueFileAgent
            :theme="'list'"
            :multiple="true"
            :maxFiles="20"
            :deletable="true"
            :class="this.fileRecordsForUpload.length > 0 ? 'vuefileagent' : ''"
            style="width: 70%; max-height: 40vh; overflow: hidden"
            v-model="fileRecords"
            @select="filesSelected($event)"
            @beforedelete="onBeforeDelete($event)"
          ></VueFileAgent>
          <b-form-input
            placeholder="ENTER EMAIL ID (OPTIONAL)"
            v-model="email"
          ></b-form-input>
          <div style="padding-top: 40px">
            <!-- <router-link to="/proof"> -->
            <b-button @click="create()" size="lg">CREATE YOUR PROOF</b-button>
            <!-- </router-link> -->

            <h4 class="error" v-show="this.bool">NO FILES UPLOADED</h4>
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
      email: "",

      dict: {},
      text: "",
      file: "",
      text1: {},
      fileRecords: [],
      uploadHeaders: { "X-Test-Header": "vue-file-agent" },
      fileRecordsForUpload: [],
      bool: false,
      loader: false,
    };
  },
  components: {
    Slides,
    Header,
  },
  updated: function () {
    this.computehash();
  },
  methods: {
    create: function () {
      if (this.fileRecordsForUpload.length == 0) {
        this.bool = true;
        return;
      }
      this.loader = true;

      let x = new Object();
      x["Files"] = this.dict;
      x["Email ID"] = this.email;

      var myHeaders = new Headers();
      myHeaders.append("Content-Type", "application/json");

      var requestOptions = {
        method: "POST",
        headers: myHeaders,
        body: JSON.stringify(x),
        redirect: "follow",
      };

      fetch("https://propre-api.herokuapp.com/propre-api/proof", requestOptions)
        .then((response) => response.json())
        .then((result) =>
          this.$router.push({ name: "Proof", params: { dict: result } })
        )
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

.vuefileagent {
  overflow: scroll !important;
}

.vuefileagent::-webkit-scrollbar {
  display: none;
  width: 0; /* Remove scrollbar space */
  background: transparent; /* Optional: just make scrollbar invisible */
  -ms-overflow-style: none; /* Internet Explorer 10+ */
  scrollbar-width: none; /* Firefox */
}

.vuefileagent {
  -ms-overflow-style: none; /* IE and Edge */
  scrollbar-width: none; /* Firefox */
}

.form-control {
  background: white;
  margin-top: 30px;
  width: 50%;
}

.create {
  display: grid;
  align-content: center;
  padding-top: 130px;
  justify-items: center;
}

.btn-secondary {
  background-color: transparent !important;
  color: #ffffff;
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
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
  /* overflow: scroll; */
}
</style>
