<template lang="">
  <div>
    <h5 class="text-bold">Female and Male Percentage</h5>
    <PieChart
      :chart-data="datacollection"
      v-if="datacollection !== null"
      :options="options"
    ></PieChart>
  </div>
</template>
<script>
import PieChart from "./PieChart.js";

export default {
  name: "FemaleMalePercentage",
  props: {
    CarData: Array
  },
  components: {
    PieChart
  },
  data() {
    return {
      datacollection: null,
      options: {
        maintainAspectRatio: false
      }
    };
  },
  mounted() {
    this.fillData();
  },
  methods: {
    fillData() {
      //I noticed there we're quite a few different genders in the json data provided
      //I'm assuming that it's just literally Female and Male by string search
      //Not that e.g. Bigender is == Female && Male

      const female = this.filterByGender("Female");
      const male = this.filterByGender("Male");

      this.datacollection = {
        labels: ["Male", "Female"],
        datasets: [
          {
            backgroundColor: ["#7ba1db", "#68d980"],
            data: [male, female]
          }
        ]
      };
    },
    filterByGender(gender) {
      const data = this.CarData;
      return data.filter(e => {
        return e.gender == gender;
      }).length;
    }
  }
};
</script>
