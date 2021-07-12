<template>
  <div id="app">
    <!-- tab -->
    <!-- form submit 01 -->
    <!-- fetch api  02 -->

    <div>
      <b-tabs content-class="mt-3">
        <b-tab title="Form" active
          ><p><HelloWorld msg="EXAM" /></p
        ></b-tab>
        <b-tab title="Fetch"
          ><p><Fetch /></p
        ></b-tab>
        <!-- data 03 -->
        <b-tab title="JSON"
          ><p>
            I'm a json tab!

            <Data /></p
        ></b-tab>
      </b-tabs>
    </div>

    <!-- <FormPage /> -->
  </div>
</template>

<script>
import Vue from "vue";
import HelloWorld from "./components/HelloWorld.vue";
// import FormPage from "./components/Form.vue";
import Fetch from "./components/Fetch.vue";
import Data from "./components/Data.vue";
import axios from "axios";
import { BootstrapVue, IconsPlugin } from "bootstrap-vue";

// Import Bootstrap an BootstrapVue CSS files (order is important)
import "bootstrap/dist/css/bootstrap.css";
import "bootstrap-vue/dist/bootstrap-vue.css";

// Make BootstrapVue available throughout your project
Vue.use(BootstrapVue);
// Optionally install the BootstrapVue icon components plugin
Vue.use(IconsPlugin);
Vue.use(axios);
export default {
  name: "App",
  components: {
    HelloWorld,
    // FormPage,
    Fetch,
    Data,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
