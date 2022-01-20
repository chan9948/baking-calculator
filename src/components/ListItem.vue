<template>
  <tr>
    <td><button @click="deleteItem">X</button></td>
    <td>
      <input
        type="text"
        :value="modelValue.itemName"
        @input="updateValue('itemName', $event.target.value)"
      />
    </td>
    <td class="inputGroup">
      <input
        min="0"
        type="number"
        :value="modelValue.percentage"
        @input="updateValue('percentage', Number($event.target.value))"
      />%
    </td>
    <td>{{ getAmount }}{{ unit }}</td>
    <td>{{ getFinalAmount }}{{ unit }}</td>
  </tr>
</template>

<script>
export default {
  name: "ListItem",
  props: {
    modelValue: Object,
    unit: String,
    mainAmount: Number,
    targetTotalAmount: Number,
    mainFinalAmount: Number,
    deleteItem: Function,
  },
  computed: {
    getAmount: function () {
      var amount = (this.modelValue.percentage * this.mainAmount) / 100;
      return amount > 0 ? amount.toFixed(1) : 0;
    },
    getFinalAmount: function () {
      var result = (this.modelValue.percentage / 100) * this.mainFinalAmount;
      return result > 0 ? result.toFixed(1) : 0;
    },
  },
  methods: {
    updateValue: function (key, value) {
      this.$emit("update:modelValue", { ...this.modelValue, [key]: value });
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
