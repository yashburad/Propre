<template>
  <div id="app">
    <div
      class="background"
      :style="{
        backgroundImage: 'url(' + require('../assets/bg2.jpg') + ')',
      }"
    >
      <div class="overlay1">
        <div class="contactus">
          <h2>We would love to hear from you!</h2>
          <b-container>
            <b-row class="mt-5 mb-5">
              <b-col>
                <b-form-input
                  v-model="first"
                  placeholder="FIRST NAME"
                ></b-form-input> </b-col
              ><b-col>
                <b-form-input
                  v-model="last"
                  placeholder="LAST NAME"
                ></b-form-input>
              </b-col>
            </b-row>
            <b-row class="mt-5 mb-5">
              <b-col>
                <b-form-input
                  v-model="email"
                  placeholder="EMAIL ID"
                ></b-form-input> </b-col
              ><b-col>
                <b-form-input
                  v-model="number"
                  placeholder="PHONE NUMBER"
                ></b-form-input>
              </b-col>
            </b-row>
            <b-row class="mt-5 mb-5">
              <b-col>
                <textarea
                  v-model="feedback"
                  class="form-control"
                  rows="5"
                  placeholder="FEEDBACK"
                ></textarea>
              </b-col>
            </b-row>
            <b-button @click="compute()" size="lg"> SUBMIT </b-button>
            <h4 class="error" style="margin-top: 20px" v-show="this.bool">
              {{ this.msg }}
            </h4>
          </b-container>
        </div>
      </div>
    </div>
    <!-- <Clipboard /> -->
    <Header heading="CONTACT US" />

    <Slides />
  </div>
</template>

<script>
import Header from "@/components/Header.vue";
import Slides from "@/components/Slides.vue";

export default {
  name: "Home",
  data() {
    return {
      first: "",
      last: "",
      email: "",
      number: "",
      feedback: "",
      bool: false,
      msg: "PLEASE FILL ALL THE DETAILS",
    };
  },
  components: {
    Slides,
    Header,
  },
  methods: {
    compute: function () {
      if (
        this.first == "" ||
        this.last == "" ||
        this.email == "" ||
        this.number == "" ||
        this.feedback == ""
      ) {
        this.bool = true;
        this.msg = "PLEASE FILL ALL THE DETAILS";
        return;
      }
      let dict = new Object();
      dict["First Name"] = this.first;
      dict["Last Name"] = this.last;
      dict["Email ID"] = this.email;
      dict["Phone"] = this.number;
      dict["Feedback"] = this.feedback;

      var myHeaders = new Headers();
      myHeaders.append("Content-Type", "application/json");

      var requestOptions = {
        method: "POST",
        headers: myHeaders,
        body: JSON.stringify(dict),
        redirect: "follow",
      };

      fetch(
        "https://propre-api.herokuapp.com/propre-api/feedback",
        requestOptions
      )
        .then((response) => response.json())
        .then((result) => {
          console.log(result);
          this.clear(result);
        })

        .catch((error) => {
          console.log("error", error);
        });
    },
    clear: function (x) {
      if (x["Status"] == true) {
        this.msg = "Submitted";
      }
      if (x["Status"] == false) {
        this.msg = x["Error"];
      }
      (this.first = ""), (this.last = "");
      this.email = "";
      this.number = "";
      this.feedback = "";
    },
  },
};
</script>

<style scoped>
a {
  color: white;
}

.contactus {
  padding-top: 25vh;
  color: white;
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

.form-control {
  border: none;
  background: white;
}

.btn-secondary {
  background-color: transparent !important;
  color: #ffffff;
  /* border-color: white; */
  padding: 0.5rem 5rem;
}

.btn-secondary:hover {
  border-color: #545b62;
}
</style>
