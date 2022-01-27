<template>
  <div id="app">
    <!-- <Chart :items="[{itemName: mainItemName, percentage: 100,},...items]"/> -->
    <br/>
    <div>
      Target Total Amount:
      <div class="inputGroup">
        <input type="number" min="0" step="0.1" v-model.number="targetTotalAmount" />
        {{ unit }}
      </div>
    </div>
    <br />
    <table>
      <tr>
        <th></th>
        <th>Item</th>
        <th>Percentage to Main</th>
        <th>Amount</th>
        <th>Target Amount</th>
      </tr>
      <tr>
        <td></td>
        <td><input type="text" v-model="mainItemName" /></td>
        <td>100%</td>
        <td>
          <div class="inputGroup">
            <input type="number" min="0" step="0.1" v-model.number="mainAmount" />
            {{ unit }}
          </div>
        </td>
        <td>
          {{ getMainFinalAmount > 0 ? getMainFinalAmount.toFixed(1) : 0 }}{{ unit }}
        </td>
      </tr>
      <ListItem
        v-for="(item, index) in items"
        v-model="items[index]"
        :key="index"
        :unit="unit"
        :mainAmount="getMainAmount"
        :targetTotalAmount="getTargetTotalAmount"
        :mainFinalAmount="getMainFinalAmount"
        :deleteItem="deleteItem.bind(index)"
      >
      </ListItem>
      <br />
    </table>
    <button @click="addItem">Add Item</button>
  </div>
</template>

<script>
import ListItem from "./components/ListItem";
// import Chart from './components/Chart';

export default {
  name: "App",
  components: {
    ListItem,
    // Chart,
  },
  data() {
    return {
      unit: "g",
      targetTotalAmount: 500,

      mainItemName: "main",
      mainAmount: 150,

      items: [
        {
          itemName: "something else",
          percentage: 10,
        },
        {
          itemName: "something else",
          percentage: 10,
        },
      ],
    };
  },
  methods: {
    deleteItem: function (index) {
      this.items.splice(index, 1);
    },
    addItem: function () {
      this.items = [
        ...this.items,
        {
          itemName: "something else",
          percentage: 10,
        },
      ];
    },
  },
  computed: {
    getMainAmount: function () {
      return this.mainAmount > 0 ? this.mainAmount : 0;
    },
    getTargetTotalAmount: function () {
      return this.targetTotalAmount > 0 ? this.targetTotalAmount : 0;
    },
    getMainFinalAmount: function () {
      var totalPercentage = 100;
      this.items.forEach((item) => {
        totalPercentage += item.percentage;
      });
      var factor = 100 * (this.targetTotalAmount / totalPercentage);
      return factor;
    },
  },
};
</script>

<style>
.inputGroup {
  border: 1px inset #000;
  display: inline-block;
  padding: 0 5px 0 0;
}
.inputGroup input {
  border: 0;
  width: 70px;
  text-align: right;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
</style>
