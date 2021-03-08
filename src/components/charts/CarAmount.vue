<template lang="">
  <div>
    <h5 class="text-bold">Car Count by Type</h5>
    <BarChart
      :chart-data="datacollection"
      v-if="datacollection !== null"
      :options="options"
    ></BarChart>
  </div>
</template>
<script>
import BarChart from "./BarChart.js";

export default {
  name: "CarAmount",
  props: {
    CarData: Array
  },
  components: {
    BarChart
  },
  data() {
    return {
      datacollection: null,
      options: {
        maintainAspectRatio: false,
        scales: {
          yAxes: [
            {
              scaleLabel: {
                display: true,
                labelString: "Amount"
              }
            }
          ]
        }
      }
    };
  },
  mounted() {
    this.fillData();
  },
  methods: {
    fillData() {
      const formattedData = this.formatData();
      this.datacollection = {
        labels: Object.keys(formattedData),
        datasets: [
          {
            label: "Car Count by Type",
            data: Object.values(formattedData)
          }
        ]
      };
    },
    formatData() {
      var carCount = [];
      this.CarData.forEach(e => {
        if (!carCount[e.car_make]) {
          carCount[e.car_make] = 1;
        } else {
          carCount[e.car_make] = carCount[e.car_make] + 1;
        }
      });
      return carCount;
    }
  }
};
</script>
