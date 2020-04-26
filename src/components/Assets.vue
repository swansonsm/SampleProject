<template>
  <div class="assets-container">
    <div class="search-container">
      <div class="search-item">
        <label for="search-name">Search </label>
        <input type="text" v-model="searchName" name="search-name" placeholder="Search assets by name...">
      </div>
      <div class="search-item">
        <label for="search-name">Filter by any of the {{ classList.size }} class names: </label>
        <select name="filter-class"
                v-model="searchClass">
          <option selected="selected"
                  :value="null">All</option>
          <option v-for="classItem in classList"
                  :key="classItem.id"
                  :value="classItem">{{ classItem.name }}</option>
        </select>
      </div>
    </div>

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
      searchName: "",
      searchClass: null
    };
  },
  computed: {
    filteredAssets() {
      let filteredList = this.filterAssetsByName();
      if (this.searchClass !== null) {
        filteredList = this.filterAssetsByClass(filteredList);
      }

      return filteredList;
    },
    classList() {
      let uniqueClassItems = new Set();
      let uniqueClassNames = new Set();
      this.assets.forEach(asset => {
        asset.classList.forEach(assetClass => {
          if (!uniqueClassNames.has(assetClass.name)) {
            uniqueClassNames.add(assetClass.name);
            uniqueClassItems.add(assetClass);
          }
        });
      });
      return uniqueClassItems;
    }
  },
  methods: {
    filterAssetsByName() {
      return this.assets
        .filter(asset => {
          return asset.name
            .toLowerCase()
            .includes(this.searchName.toLowerCase());
        })
        .sort((a, b) => (a.status < b.status ? 1 : -1));
    },
    filterAssetsByClass(filteredList) {
      return filteredList.filter(asset => {
        return asset.classList.some(assetClass => {
          return assetClass.name == this.searchClass.name;
        });
      });
    }
  }
};
</script>

<style>
.assets-container {
  width: 80%;
  margin: 12px auto;
}
.search-container {
  margin: 12px;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
.search-item {
  padding: 6px;
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
