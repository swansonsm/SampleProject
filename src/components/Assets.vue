<template>
  <div class="assets-container">
    <input type="text" v-model="searchName" name="search-name" placeholder="Search assets...">

    <div class="row header">
      <div class="col-id"> Asset ID </div>
      <div class="col-name"> Name </div>
      <div class="col-description"> Description </div>
      <div class="col-status"> Status </div>
    </div>

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

<style>
.assets-container {
  width: 80%;
  margin: auto;
}
input {
  width: 250px;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  margin: 0 10px;
}
.header div {
  font-weight: bold;
}
.item div {
  font-weight: normal;
}
.row {
  width: 100%;
  display: inline-flex;
}
.col-id {
  width: 10%;
  text-align: left;
}
.col-name {
  width: 40%;
  text-align: left;
}
.col-description {
  width: 40%;
  text-align: left;
}
.col-status {
  width: 10%;
}
</style>
