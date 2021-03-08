<template lang="">
  <div>
    <h5 class="text-bold">Car Age Grouped By Decade</h5>
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
  name: "FemaleMalePercentage",
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
          ],
          xAxes: [
            {
              scaleLabel: {
                display: true,
                labelString: "Decade"
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
        labels: [...formattedData.keys()],
        datasets: [
          {
            label: "Amount",
            data: formattedData,
            barPercentage: 1.0,
            categoryPercentage: 6.0
          }
        ]
      };
    },
    formatData() {
      var groupedByDecade = [];
      this.CarData.forEach(e => {
        const decade = Math.floor(e.age / 10) * 10;
        if (!groupedByDecade[decade]) {
          groupedByDecade[decade] = 1;
        } else {
          groupedByDecade[decade] = groupedByDecade[decade] + 1;
        }
      });

      return groupedByDecade;
    }
  }
};
</script>
