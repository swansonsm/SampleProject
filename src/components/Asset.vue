<template>
  <div class="row">
    <span> {{ asset.assetId }} </span>
    <span> {{ asset.name }} </span>
    <span> {{ asset.description }} </span>
    <span> {{ asset.status }} </span>
  </div>
</template>

<script>
export default {
  name: "Asset",
  props: {
    asset: {
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
