<template>
  <div class="assets-container">
    <Asset v-for="asset in assets"
           :key="asset.assetId"
           v-bind:asset="asset"></Asset>
  </div>
</template>

<script>
import Asset from "./Asset.vue";

export default {
  name: "Assets",
  components: {
    Asset
  },
  props: {
    assets: {
      type: Array,
      default: () => []
    }
  }
};
</script>

<style scoped>
.assets-container {
  width: 80%;
  margin: auto;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
