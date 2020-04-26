<template>
  <div class="row">
    <span> {{ asset.assetId }} </span>
    <span> {{ asset.name }} </span>
    <span> {{ asset.description }} </span>
    <StatusLabel v-bind:status="asset.status"
                 v-bind:assetStatus="assetStatus"></StatusLabel>
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
.row {
  width: 100%;
  display: inline-flex;
  justify-content: space-between;
}
</style>
