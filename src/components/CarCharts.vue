<template lang="">
  <div class="w-full mb-10">
    <div class="flex flex-row">
      <div class="w-50">
        <FemaleMaleChart :car-data="CarData"></FemaleMaleChart>
      </div>
      <div class="w-50">
        <AgeGrouped :car-data="CarData"></AgeGrouped>
      </div>
    </div>
    <div class="flex flex-row mt-10">
      <CarAmount :car-data="CarData"></CarAmount>
    </div>
  </div>
</template>
<script>
import FemaleMaleChart from "./charts/FemaleMalePercentage";
import AgeGrouped from "./charts/AgeGrouped";
import CarAmount from "./charts/CarAmount";

export default {
  name: "CarTable",
  props: {
    CarData: Array
  },
  components: {
    FemaleMaleChart,
    AgeGrouped,
    CarAmount
  }
};
</script>
<style lang=""></style>
