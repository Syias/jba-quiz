<template>
  <div class="m-auto">
    <table class="table-auto text-left m-4 w-full">
      <thead>
        <tr class="bg-gray-100">
          <th
            v-for="field in fields"
            :key="field.key"
            class="py-4 px-6 font-medium border-b"
            @click="filter(field.key)"
          >
            {{ field.label }}
          </th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="car in paginatedData"
          :key="car.id"
          class="hover:bg-gray-100 border-b"
        >
          <td class="py-2 px-4 text-center">{{ car.id }}</td>
          <td class="py-2 px-4 text-center">{{ car.name }}</td>
          <td class="py-2 px-4 text-center">{{ car.email }}</td>
          <td class="py-2 px-4 text-center">{{ car.gender }}</td>
          <td class="py-2 px-4 text-center">{{ car.age }}</td>
          <td class="py-2 px-4 text-center">{{ car.car_make }}</td>
        </tr>
      </tbody>
    </table>
    <button
      @click="prevPage"
      class="p-4 mx-4 border border-grey bg-gray-300 hover:bg-gray-200 rounded-md"
    >
      Previous
    </button>
    <button
      @click="nextPage"
      class="p-4 mx-4 border border-grey bg-gray-300 hover:bg-gray-200 rounded-md"
    >
      Next
    </button>
  </div>
</template>
<script>
export default {
  /**
   * Did some of it manully, then moved to bootstrap as its 10x faster
   */
  name: "CarTable",
  props: {
    CarData: Array
  },
  data() {
    return {
      fields: [
        { key: "id", label: "ID" },
        { key: "name", label: "Name" },
        { key: "email", label: "Email" },
        { key: "gender", label: "Gender" },
        { key: "age", label: "Age" },
        { key: "car_make", label: "Car Make" }
      ],
      pageNumber: 0,
      size: 10,
      copiedData: this.CarData
    };
  },
  methods: {
    nextPage() {
      this.pageNumber++;
    },
    prevPage() {
      if (this.pageNumber >= 1) {
        this.pageNumber--;
      }
    }
  },
  computed: {
    paginatedData() {
      const start = this.pageNumber * this.size,
        end = start + this.size;
      return this.copiedData.slice(start, end);
    },
    pageCount() {
      let l = this.copiedData.length,
        s = this.size;
      return Math.ceil(l / s);
    }
  }
};
</script>
