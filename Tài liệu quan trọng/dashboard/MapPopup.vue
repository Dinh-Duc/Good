<template>
  <div class="space-y-16">
    <div
      class="ykien-item flex items-center space-x-16"
    >
      <div class="ykien-item__content">Loại: {{ feature.properties.name }}</div>
      <div class="ykien-item__content">Tọa độ: {{ feature.geometry.coordinates }}</div>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
export default Vue.extend({
  name: "MapPopup",
  props: {
    feature: {
      required: true,
      type: Object,
      default: null,
    },
  },
  methods: {},
});
</script>