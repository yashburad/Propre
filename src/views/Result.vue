<template>
  <div id="app">
    <div
      class="background"
      :style="{
        backgroundImage: 'url(' + require('../assets/bg2.jpg') + ')',
      }"
    >
      <div class="overlay1">
        <b-container style="margin-top: 100px">
          <b-row class="d-block" v-if="this.result">
            <div class="ui-success">
              <svg
                style="width: 200px"
                viewBox="0 0 87 87"
                version="1.1"
                xmlns="http://www.w3.org/2000/svg"
                xmlns:xlink="http://www.w3.org/1999/xlink"
              >
                <g
                  id="Page-1"
                  stroke="none"
                  stroke-width="1"
                  fill="none"
                  fill-rule="evenodd"
                >
                  <g id="Group-3" transform="translate(2.000000, 2.000000)">
                    <circle
                      id="Oval-2"
                      stroke="#4bb71b"
                      stroke-width="4"
                      cx="41.5"
                      cy="41.5"
                      r="41.5"
                    ></circle>
                    <circle
                      class="ui-success-circle"
                      id="Oval-2"
                      stroke="#4bb71b"
                      stroke-width="4"
                      cx="41.5"
                      cy="41.5"
                      r="41.5"
                    ></circle>
                    <polyline
                      class="ui-success-path"
                      id="Path-2"
                      stroke="#4bb71b"
                      stroke-width="4"
                      points="19 38.8036813 31.1020744 54.8046875 63.299221 28"
                    ></polyline>
                  </g>
                </g>
              </svg>
            </div>
            <h2 style="color: white; padding-top: 50px">
              VERIFICATION SUCCESSFUL
            </h2>
          </b-row>
          <b-row class="d-block" v-else>
            <div class="ui-error">
              <svg
                style="width: 200px"
                viewBox="0 0 87 87"
                version="1.1"
                xmlns="http://www.w3.org/2000/svg"
                xmlns:xlink="http://www.w3.org/1999/xlink"
              >
                <g
                  id="Page-1"
                  stroke="none"
                  stroke-width="1"
                  fill="none"
                  fill-rule="evenodd"
                >
                  <g id="Group-2" transform="translate(2.000000, 2.000000)">
                    <circle
                      id="Oval-2"
                      stroke="#F74444"
                      stroke-width="4"
                      cx="41.5"
                      cy="41.5"
                      r="41.5"
                    ></circle>
                    <circle
                      class="ui-error-circle"
                      stroke="#F74444"
                      stroke-width="4"
                      cx="41.5"
                      cy="41.5"
                      r="41.5"
                    ></circle>
                    <path
                      class="ui-error-line1"
                      d="M22.244224,22 L60.4279902,60.1837662"
                      id="Line"
                      stroke="#F74444"
                      stroke-width="3"
                      stroke-linecap="square"
                    ></path>
                    <path
                      class="ui-error-line2"
                      d="M60.755776,21 L23.244224,59.8443492"
                      id="Line"
                      stroke="#F74444"
                      stroke-width="3"
                      stroke-linecap="square"
                    ></path>
                  </g>
                </g>
              </svg>
            </div>
            <h2 style="color: white; padding-top: 50px">VERIFICATION FAILED</h2>
            <h4
              class="animate__shakeX animate__animated"
              style="color: white; padding-top: 50px"
            >
              {{ this.message }}
            </h4>
          </b-row>
        </b-container>
      </div>
    </div>
    <Header heading="RESULT" />
    <Slides />
  </div>
</template>

<script>
import Header from "@/components/Header.vue";
import Slides from "@/components/Slides.vue";

// import VueFileAgent from 'vue-file-agent';

export default {
  name: "Result",

  data() {
    return {
      dict: this.$route.params.proof,
      result: this.$route.params.proof.verify,
      message: "",
    };
  },
  components: {
    Slides,
    Header,
  },
  mounted: function () {
    if (this.dict["Status"] == false) {
      this.message = this.dict["Error"];
    }
  },
};
</script>

<style scoped>
.demo1 {
  height: 300px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.ui-success,
.ui-error {
  margin: 40px;
}
.ui-success-circle {
  stroke-dasharray: 260.752190248px, 260.752190248px;
  stroke-dashoffset: 260.752190248px;
  transform: rotate(220deg);
  transform-origin: center center;
  stroke-linecap: round;
  animation: ani-success-circle 1s ease-in both;
}
.ui-success-path {
  stroke-dasharray: 60px 64px;
  stroke-dashoffset: 62px;
  stroke-linecap: round;
  animation: ani-success-path 0.4s 1s ease-in both;
}
@keyframes ani-success-circle {
  to {
    stroke-dashoffset: 782.2565707439px;
  }
}
@keyframes ani-success-path {
  0% {
    stroke-dashoffset: 62px;
  }
  65% {
    stroke-dashoffset: -5px;
  }
  84% {
    stroke-dashoffset: 4px;
  }
  100% {
    stroke-dashoffset: -2px;
  }
}
.ui-error-circle {
  stroke-dasharray: 260.752190248px, 260.752190248px;
  stroke-dashoffset: 260.752190248px;
  animation: ani-error-circle 1.2s linear;
}
.ui-error-line1 {
  stroke-dasharray: 54px 55px;
  stroke-dashoffset: 55px;
  stroke-linecap: round;
  animation: ani-error-line 0.15s 1.2s linear both;
}
.ui-error-line2 {
  stroke-dasharray: 54px 55px;
  stroke-dashoffset: 55px;
  stroke-linecap: round;
  animation: ani-error-line 0.2s 0.9s linear both;
}
@keyframes ani-error-line {
  to {
    stroke-dashoffset: 0;
  }
}
@keyframes ani-error-circle {
  0% {
    stroke-dasharray: 0, 260.752190248px;
    stroke-dashoffset: 0;
  }
  35% {
    stroke-dasharray: 120px, 120px;
    stroke-dashoffset: -120px;
  }
  70% {
    stroke-dasharray: 0, 260.752190248px;
    stroke-dashoffset: -260.752190248px;
  }
  100% {
    stroke-dasharray: 260.752190248px, 0;
    stroke-dashoffset: -260.752190248px;
  }
}

.create {
  display: grid;
  align-content: center;
  padding-top: 130px;
  justify-items: center;
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

.contain {
  height: 100%;
  align-items: center;
  justify-content: center;
  color: white;
}

.success-animation {
  margin-bottom: 50px;
}

.checkmark {
  width: 200px;
  height: 200px;
  border-radius: 50%;
  display: block;
  stroke-width: 2;
  stroke: #4bb71b;
  stroke-miterlimit: 10;
  box-shadow: inset 0px 0px 0px #4bb71b;
  animation: fill 0.4s ease-in-out 0.4s forwards,
    scale 0.3s ease-in-out 0.9s both;
  position: relative;
  top: 5px;
  right: 5px;
  margin: 0 auto;
}
.checkmark__circle {
  stroke-dasharray: 166;
  stroke-dashoffset: 166;
  stroke-width: 2;
  stroke-miterlimit: 10;
  stroke: #4bb71b;
  fill: #fff;
  animation: stroke 0.6s cubic-bezier(0.65, 0, 0.45, 1) forwards;
}

.checkmark__check {
  transform-origin: 50% 50%;
  stroke-dasharray: 48;
  stroke-dashoffset: 48;
  animation: stroke 0.3s cubic-bezier(0.65, 0, 0.45, 1) 0.8s forwards;
}

@keyframes stroke {
  100% {
    stroke-dashoffset: 0;
  }
}

@keyframes scale {
  0%,
  100% {
    transform: none;
  }

  50% {
    transform: scale3d(1.1, 1.1, 1);
  }
}

@keyframes fill {
  100% {
    box-shadow: inset 0px 0px 0px 30px #4bb71b;
  }
}
</style>
