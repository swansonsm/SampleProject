<template>
  <div id="app">
    <h1>TwinThread Coding Challenge</h1>
    <input type="file" id="dataUploader" @change="loadData">
    <Assets v-if="assets.length > 0"
            v-bind:assets="assets"
            v-bind:asset-status="asset_status"
            v-bind:data-type="dataType"/>
  </div>
</template>

<script>
import Assets from "./components/Assets.vue";

export default {
  name: "App",
  components: {
    Assets
  },
  data() {
    return {
      assets: [],
      asset_status: {},
      dataType: {}
    };
  },
  methods: {
    loadData(event) {
      var files = event.target.files;

      if (files.length <= 0) {
        return false;
      }

      const fr = new FileReader();

      fr.onload = e => {
        const result = JSON.parse(e.target.result);
        this.assets = result.assets;
        this.asset_status = result.asset_status;
        this.dataType = result.dataType;
      };
      fr.readAsText(files.item(0));
    }
  }
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
