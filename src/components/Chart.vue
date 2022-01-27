<template>
  <div class="chart">
    <ChartChild v-for="(item, index) in items" :key="index" :item="item" />
  </div>
</template>
<script>
import ChartChild from "./ChartChild";
export default {
  components: {
    ChartChild,
  },
  props: {
    items: Object,
  },
  computed: {},
};
</script>
<style>
.chart {
  border-radius: 5px;
  background-color: red;
  display: flex;
  flex-wrap: nowrap;
}
</style>
