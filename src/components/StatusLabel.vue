<template>
  <span class="label"
        v-bind:class="statusClass">{{ statusText }}</span>
</template>

<script>
export default {
  name: "StatusLabel",
  props: {
    status: {
      type: Number
    },
    assetStatus: {
      type: Object,
      default: () => {}
    }
  },
  data: function() {
    return {};
  },
  computed: {
    statusClass() {
      let statusClass = "";
      if (this.status === 1) {
        statusClass = "label-success";
      } else if (this.status === 2) {
        statusClass = "label-warning";
      } else if (this.status === 3) {
        statusClass = "label-danger";
      }
      return statusClass;
    },
    statusText() {
      let statusText = "";
      if (this.status === 1) {
        statusText = "Normal";
      } else if (this.status === 2) {
        statusText = "Warning";
      } else if (this.status === 3) {
        statusText = "Critical";
      }
      return statusText;
    }
  },
  methods: {}
};
</script>

<style scoped>
.label {
  display: inline;
  padding: 0.2em 0.6em 0.3em;
  font-size: 75%;
  font-weight: 700;
  line-height: 1;
  color: #fff;
  text-align: center;
  white-space: nowrap;
  vertical-align: baseline;
  border-radius: 0.25em;
}
.label-success {
  background-color: #5cb85c;
}
.label-warning {
  background-color: #f0ad4e;
}
.label-danger {
  background-color: #d9534f;
}
</style>
