<template>
  <div id="app">
    <div
      class="background"
      :style="{
        backgroundImage: 'url(' + require('../assets/bg2.jpg') + ')',
      }"
    >
      <div class="overlay1">
        <div class="create">
          <VueFileAgent
            :theme="'list'"
            :multiple="true"
            :maxFiles="20"
            :deletable="true"
            :class="
              this.fileRecordsForUpload.length > 0
                ? 'animate__animated animate__fadeInDown vuefileagent'
                : 'animate__animated animate__fadeInDown'
            "
            style="
              animation-duration: 5s;
              width: 70%;
              max-height: 40vh;
              overflow: hidden;
            "
            v-model="fileRecords"
            @select="filesSelected($event)"
            @beforedelete="onBeforeDelete($event)"
          ></VueFileAgent>
          <b-form-input
            placeholder="ENTER EMAIL ID (OPTIONAL)"
            v-model="email"
          ></b-form-input>
          <div style="padding-top: 40px">
            <router-link to="/proof">
              <b-button size="lg">CREATE YOUR PROOF</b-button>
            </router-link>
            <b-button
              size="lg"
              @click="
                computehash();
                create();
              "
            >
              Create Your Proof
            </b-button>
          </div>
        </div>
      </div>
    </div>
    <h1>{{ this.info }}aa</h1>
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
      info: null,
      email: "",
      dict: {},
      text: "",
      file: "",
      text1: {},
      fileRecords: [],
      uploadHeaders: { "X-Test-Header": "vue-file-agent" },
      fileRecordsForUpload: [],
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
      // const keys = Object.keys(this.dict);
      // console.log(keys);
      // let a = "";
      // for (var i in keys) {
      //   a += keys[i] + "+";
      // }
      // a = a.substring(0, a.length - 1);
      // let b = "";
      // for (i in this.dict) {
      //   // console.log(this.dict[i]);
      //   b += this.dict[i] + "+";
      // }
      // b = b.substring(0, b.length - 1);
      // console.log(b);
      // console.log(a);
      // let str = "http://127.0.0.1:5000/propre/api?files=" + a + "&hashes=" + b;
      // let str1 =
      //   "http://127.0.0.1:5000/propre/api?files=abcd.c+ghghgg.out&hashes=abcdabcd+abcdabcd";
      // var requestOptions = {
      //   method: "POST",
      //   headers: { "Content-Type": "application/json" },
      //   mode: "no-cors",
      // };
      // fetch(str1, requestOptions).then((response) =>
      //   console.log(response.json)
      // );
      // var requestOptions = {
      //   method: "POST",
      //   redirect: "follow",
      //   mode: "no-cors",
      // };
      // let a = {};
      // fetch("http://127.0.0.1:5000/", requestOptions).then((response) =>
      //   console.log(response.json())
      // );
      // console.log(a);
      // var requestOptions = {
      //   method: "get",
      //   redirect: "follow",
      //   mode: "no-cors",
      //   headers: { "Content-Type": "text/plain" },
      // };
      // fetch("https://api.npms.io/v2/search?q=vue", requestOptions)
      //   .then((response) => response.json())
      //   .then((response) => console.log(response))
      //   .catch((error) => console.log("error", error));
      // var myHeaders = new Headers();
      // myHeaders.append("Access-Control-Allow-Origin", "http://localhost:8000");
      // var requestOptions = {
      //   method: "GET",
      //   headers: myHeaders,
      //   redirect: "follow",
      //   mode: "no-cors",
      // };
      // fetch("https://learnercircle.herokuapp.com")
      //   .then((response) => response.text())
      //   .then((result) => console.log(result))
      //   .catch((error) => console.log("error", error));var myHeaders = new Headers();
      // var myHeaders = new Headers();
      // myHeaders.append("Access-Control-Allow-Origin", "*");
      // var axios = require("axios");
      // axios
      //   .get("http://127.0.0.1:5000/")
      //   .then((response) => (this.info = response));
      // var requestOptions = {
      //   method: "get",
      //   mode: "no-cors",
      // };
      fetch(
        "https://propre-api.herokuapp.com/propre/api?files=aa.out&hashes=aa"
      )
        .then((response) => response.json())
        .then((response) => (this.info = response))
        .catch((error) => console.log("error", error));
      console.log(this.info);
      // let body;
      // .then((result) => console.log(result))
      // .catch((error) => console.log("error", error));
      // .then((result) => console.log(result))
      // .catch((error) => console.log(this.dict, error));
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
.vuefileagent {
  overflow: scroll !important;
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
