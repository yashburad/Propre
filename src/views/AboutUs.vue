<template>
  <div id="app">
    <div
      class="background"
      :style="{
        backgroundImage: 'url(' + require('../assets/bg2.jpg') + ')',
      }"
    >
      <div class="overlay1">
        <div class="aboutus">
          <b-container
            class="animate__animated animate__fadeIn"
            style="padding: 20px 0px; animation-duration: 4s"
          >
            <h1 style="margin-bottom: 30px">About the Project</h1>

            <b-row>
              <p style="text-align: justify">
                Propre (standing for Proof Of Presence) is an application that
                allows you to verify the authenticity of your documents and
                files. For example, you need to share a letter to someone who
                might share it with a third party. You develop the letter and
                upload it under Create Your Proof on Propre. You receive a
                Transaction ID and File Path for that file. You can now send
                this letter to that person who can share with it the concerned
                third parties. You can make this transaction ID and file path
                public. The third party can upload the letter under Verification
                on Propre along with the transaction ID and file hash that you
                had made public earlier. If the letter is unaltered, they will
                receive a success status, or a failed status otherwise.
              </p>
            </b-row>
          </b-container>
          <b-container
            class="animate__animated animate__fadeInUp"
            style="
              margin-top: 30px;
              padding-bottom: 50px;
              animation-duration: 4s;
            "
          >
            <h1 style="margin-bottom: 50px">Founders</h1>
            <b-row>
              <b-col class="images">
                <img src="../assets/yash.jpg" />
                <h2>Yash Burad</h2>
                <div>
                  <a
                    href="https://www.linkedin.com/in/yash-burad-6aa443177/"
                    target="_blank"
                  >
                    <i
                      class="fa fa-linkedin-square"
                      style="font-size: 28px; margin-right: 20px"
                    ></i>
                  </a>
                  <a href="https://github.com/yashburad" target="_blank">
                    <i
                      class="fa fa-github"
                      style="font-size: 28px"
                      aria-hidden="true"
                    ></i>
                  </a>
                </div>
              </b-col>
              <b-col class="images">
                <img src="../assets/yvj.jpg" />
                <h2>Yashvardhan Jain</h2>
                <div>
                  <a
                    href="https://www.linkedin.com/in/yashvardhanjain-yvj/"
                    target="_blank"
                  >
                    <i
                      class="fa fa-linkedin-square"
                      style="font-size: 28px; margin-right: 20px"
                    ></i>
                  </a>
                  <a href="https://github.com/IamYVJ" target="_blank">
                    <i
                      class="fa fa-github"
                      style="font-size: 28px"
                      aria-hidden="true"
                    ></i>
                  </a>
                </div>
              </b-col>
            </b-row>
          </b-container>
          <b-container
            class="animate__animated animate__fadeInUp"
            style="
              margin-top: 30px;
              padding-bottom: 50px;
              animation-duration: 4s;
            "
          >
            <h1 style="margin-bottom: 50px">Mentor</h1>

            <b-row>
              <b-col class="images">
                <img style="height: 50vh" src="../assets/prof.jpg" />
                <h2>PROF. MAHAVIR JHAWAR</h2>
              </b-col>
            </b-row>
          </b-container>
        </div>
      </div>
    </div>
    <!-- <Clipboard /> -->
    <Header heading="ABOUT US" />

    <Slides />
  </div>
</template>

<script>
import Header from "@/components/Header.vue";
import Slides from "@/components/Slides.vue";

export default {
  name: "Home",
  data() {
    return {};
  },
  components: {
    Slides,
    Header,
  },
  methods: {},
};
</script>

<style scoped>
a {
  color: white;
}

.images h2 {
  margin-top: 20px;
}

.about-data {
  display: flex;
  justify-content: center;
}

.aboutus img {
  height: 60vh;
  margin: 0px 40px;
  filter: grayscale(1);
}

.aboutus {
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
</style>
