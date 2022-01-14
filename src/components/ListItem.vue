<template>
  <tr>
    <td><button @click="deleteItem">X</button></td>
    <td><input type="text" v-model="value.itemName" /></td>
    <td class="inputGroup">
      <input min="0" type="number" v-model.number="value.percentage" />%
    </td>
    <td>{{ getAmount }}{{ unit }}</td>
    <td>{{ getFinalAmount }}{{ unit }}</td>
  </tr>
</template>

<script>
export default {
  name: "ListItem",
  props: {
    value: Object,
    unit: String,
    mainAmount: Number,
    targetTotalAmount: Number,
    mainFinalAmount: Number,
    deleteItem: Function,
  },
  computed: {
    getAmount: function () {
      var amount = (this.value.percentage * this.mainAmount) / 100;
      return amount > 0 ? amount.toFixed(1) : 0;
    },
    getFinalAmount: function () {
      var result = (this.value.percentage / 100) * this.mainFinalAmount;
      return result > 0 ? result.toFixed(1) : 0;
    },
  },
};
</script>

<style>
.inputGroup {
  border: 1px inset #000;
  display: inline-block;
  padding: 0 5px 0 0;
  white-space: nowrap;
}
.inputGroup input {
  border: 0;
  width: 70px;
  text-align: right;
}
</style>