<template id="t">
  <b-container>
    <b-row>
      <b-col class="filename" md="2">
        <h5>{{ this.dict.fileName + "'s path" }} :</h5>
      </b-col>
      <b-col class="filepath" md="9">
        <b-form-input
          class="w-100"
          :value="this.dict.path"
          readonly
        ></b-form-input>
        <!-- <h5>{{ " " + this.dict.path }}</h5> -->
      </b-col>
      <b-col md="1" @click="doCopy" v-bind:title="message"
        ><svg
          xmlns="http://www.w3.org/2000/svg"
          width="16"
          height="16"
          fill="currentColor"
          class="bi bi-clipboard"
          viewBox="0 0 16 16"
        >
          <path
            d="M4 1.5H3a2 2 0 0 0-2 2V14a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V3.5a2 2 0 0 0-2-2h-1v1h1a1 1 0 0 1 1 1V14a1 1 0 0 1-1 1H3a1 1 0 0 1-1-1V3.5a1 1 0 0 1 1-1h1v-1z"
          />
          <path
            d="M9.5 1a.5.5 0 0 1 .5.5v1a.5.5 0 0 1-.5.5h-3a.5.5 0 0 1-.5-.5v-1a.5.5 0 0 1 .5-.5h3zm-3-1A1.5 1.5 0 0 0 5 1.5v1A1.5 1.5 0 0 0 6.5 4h3A1.5 1.5 0 0 0 11 2.5v-1A1.5 1.5 0 0 0 9.5 0h-3z"
          /></svg
      ></b-col>
      <!-- <div @click="doCopy" v-bind:title="message" class="clipboard">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="16"
          height="16"
          fill="currentColor"
          class="bi bi-clipboard"
          viewBox="0 0 16 16"
        >
          <path
            d="M4 1.5H3a2 2 0 0 0-2 2V14a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V3.5a2 2 0 0 0-2-2h-1v1h1a1 1 0 0 1 1 1V14a1 1 0 0 1-1 1H3a1 1 0 0 1-1-1V3.5a1 1 0 0 1 1-1h1v-1z"
          />
          <path
            d="M9.5 1a.5.5 0 0 1 .5.5v1a.5.5 0 0 1-.5.5h-3a.5.5 0 0 1-.5-.5v-1a.5.5 0 0 1 .5-.5h3zm-3-1A1.5 1.5 0 0 0 5 1.5v1A1.5 1.5 0 0 0 6.5 4h3A1.5 1.5 0 0 0 11 2.5v-1A1.5 1.5 0 0 0 9.5 0h-3z"
          />
        </svg>
      </div> -->
    </b-row>
  </b-container>
  <!-- <div style="display: contents" class="app">
    <div>
      <h5>{{ this.dict.fileName + "'s path" }}</h5>
    </div>
    <h5>:</h5>
    <div style="overflow-wrap: anywhere">
      <h5>{{ " " + this.dict.path }}</h5>
    </div>
    <div @click="doCopy" v-bind:title="message" class="clipboard">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        width="16"
        height="16"
        fill="currentColor"
        class="bi bi-clipboard"
        viewBox="0 0 16 16"
      >
        <path
          d="M4 1.5H3a2 2 0 0 0-2 2V14a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V3.5a2 2 0 0 0-2-2h-1v1h1a1 1 0 0 1 1 1V14a1 1 0 0 1-1 1H3a1 1 0 0 1-1-1V3.5a1 1 0 0 1 1-1h1v-1z"
        />
        <path
          d="M9.5 1a.5.5 0 0 1 .5.5v1a.5.5 0 0 1-.5.5h-3a.5.5 0 0 1-.5-.5v-1a.5.5 0 0 1 .5-.5h3zm-3-1A1.5 1.5 0 0 0 5 1.5v1A1.5 1.5 0 0 0 6.5 4h3A1.5 1.5 0 0 0 11 2.5v-1A1.5 1.5 0 0 0 9.5 0h-3z"
        />
      </svg>
    </div>
  </div> -->
</template>

<script>
export default {
  name: "Clipboard",

  props: {
    dict: new Object(),
  },
  data: function () {
    return {
      message: "Copy the path to the Clipboard",
    };
  },
  methods: {
    doCopy: function () {
      this.$copyText(this.dict.path).then(
        function (e) {
          alert("Copied");
          console.log(e);
        },
        function (e) {
          alert("Can not copy");
          console.log(e);
        }
      );
    },
  },
};
</script>

<style scoped>
.form-control {
  background: transparent;
  color: white;
  text-transform: uppercase;
}
.clipboard {
  position: relative;
  top: -25px;
  right: 0px;
  cursor: pointer;
}
.filename h5 {
  overflow-wrap: break-word;
}

.filepath {
  overflow: scroll;
}
</style>
