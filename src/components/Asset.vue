<template>
  <div class="row">
    <div class="col-id"> {{ asset.assetId }} </div>
    <div class="col-name"> {{ asset.name }} </div>
    <div class="col-description"> {{ asset.description }} </div>
    <div class="col-status">
      <StatusLabel v-bind:status="asset.status"
                   v-bind:assetStatus="assetStatus"></StatusLabel>
    </div>
    
  </div>
</template>

<script>
import StatusLabel from "./StatusLabel.vue";

export default {
  name: "Asset",
  components: {
    StatusLabel
  },
  props: {
    asset: {
      type: Object,
      default: () => {}
    },
    assetStatus: {
      type: Object,
      default: () => {}
    },
    dataType: {
      type: Object,
      default: () => {}
    }
  }
};
</script>

<style scoped>
</style>
