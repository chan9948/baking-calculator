<template>
  <div
    :style="{ width: item.percentage + '%', backgroundColor: getColor }"
    class="chartChild"
  >
    {{ item.itemName }}
    {{ item.percentage + "%" }}
  </div>
</template>
<script>
export default {
  props: {
    item: Object,
  },
  computed: {
    getColor: function () {
      let letters = "56789";
      let color = "#";
      for (var i = 0; i < 6; i++) {
        color += letters[Math.floor(Math.random() * letters.length)];
      }
      console.log(color);
      return color;
    },
  },
};
</script>
<style>
.chartChild {
  display: inline-block;
  padding: 10px;
  transition: width 1s ease;
  color: white;
  border-radius: 5px;
}
</style>
