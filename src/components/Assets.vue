<template>
  <div class="assets-container">
    <input type="text" v-model="searchName" name="search-name" placeholder="Search assets...">
    <Asset v-for="asset in filteredAssets"
           :key="asset.assetId"
           v-bind:asset="asset"
           v-bind:asset-status="assetStatus"
           v-bind:data-type="dataType"></Asset>
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
    },
    assetStatus: {
      type: Object,
      default: () => {}
    },
    dataType: {
      type: Object,
      default: () => {}
    }
  },
  data: function() {
    return {
      searchName: ""
    };
  },
  computed: {
    filteredAssets() {
      return this.assets
        .filter(asset => {
          return asset.name
            .toLowerCase()
            .includes(this.searchName.toLowerCase());
        })
        .sort((a, b) => (a.status < b.status ? 1 : -1));
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
