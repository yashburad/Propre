<template>
  <div v-show="imgIsLoaded" id="app">
    <div
      class="background"
      :style="{
        backgroundImage: 'url(' + require('../assets/bg2.jpg') + ')',
      }"
    >
      <div v-show="imgIsLoaded" class="overlay">
        <div
          class="animate__fadeIn"
          style="display: grid; animation-duration: 7s"
        >
          <div>
            <img
              :class="imgIsLoaded ? 'show' : ''"
              @load="imgLoadedMethod"
              src="../assets/logo4-min.png"
            />
          </div>
          <router-link to="/create">
            <b-button size="lg">CREATE YOUR PROOF</b-button>
          </router-link>
        </div>
      </div>
    </div>
    <Slides />
  </div>
</template>

<script>
// import Header from "@/components/Header.vue";
import Slides from "@/components/Slides.vue";

export default {
  name: "Home",
  data() {
    return {
      imgIsLoaded: false,
    };
  },
  components: {
    Slides,
  },
  methods: {
    imgLoadedMethod() {
      this.imgIsLoaded = true;
    },
  },
};
</script>

<style scoped>
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
  height: 100vh;
  background-size: 100% 100%;
}
.overlay {
  position: relative;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: #00000000;
  display: grid;
  align-items: center;
}

.show {
  opacity: 0;
}

.show {
  opacity: 1;
  height: 200px;
  justify-self: center;
}

@keyframes mymove {
  from {
    /* background-color: #00000000; */
    opacity: 0;
  }
  to {
    opacity: 1;
    /* background-color: #0000007c; */
  }
}

.contain {
  height: 100%;
  align-items: center;
  justify-content: center;
  color: white;
}

.theme-undefined {
  display: flow-root;
  width: 70%;
  justify-self: center;
}
</style>
