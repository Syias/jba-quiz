<template>
  <div id="app">
    <div
      class="container mx-auto flex-col h-100 bg-white mt-3 mb-3 pb-6 pt-6 shadow-lg"
    >
      <div class="w-full py-8 flex flex-wrap px-16">
        <button
          class="py-6 px-10 mx-auto rounded-md bg-blue-500 hover:bg-blue-600 align-middle text-white"
          @click="actionShowTable(true)"
        >
          Show Table
        </button>
        <button
          class="py-6 px-10 mx-auto rounded-md bg-gray-500 hover:bg-gray-600 text-white"
          @click="actionShowTable(false)"
        >
          Show Chart
        </button>
      </div>
      <div class="w-full">
        <CarTable :car-data="jsonCarData" v-if="showTable"></CarTable>
        <CarCharts :car-data="jsonCarData" v-if="!showTable"></CarCharts>
      </div>
    </div>
  </div>
</template>

<script>
import CarTable from "./components/CarTable";
import CarData from "./assets/data/quiz.json";
import CarCharts from "./components/CarCharts";
export default {
  name: "App",
  components: {
    CarTable,
    CarCharts
  },
  data() {
    return {
      jsonCarData: CarData,
      showTable: true
    };
  },
  methods: {
    actionShowTable(shouldShow) {
      this.showTable = shouldShow;
    }
  }
};
</script>
