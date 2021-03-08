<template>
  <div class="m-auto">
    <b-form-group
      label="Filter by Age"
      label-for="filter-input"
      label-cols-sm="3"
      label-align-sm="right"
      label-size="sm"
      class="mb-2"
    >
      <b-input-group size="sm">
        <b-form-input
          id="filter-input"
          v-model="filter"
          type="search"
          placeholder="Type to Search"
        ></b-form-input>

        <b-input-group-append>
          <b-button :disabled="!filter" @click="filter = ''">Clear</b-button>
        </b-input-group-append>
      </b-input-group>
    </b-form-group>

    <b-table
      striped
      hover
      :items="CarData"
      :fields="fields"
      :per-page="perPage"
      :current-page="currentPage"
      :filter="filter"
      :filter-included-fields="['age']"
      @filtered="onFiltered"
    >
      <template #cell(show_details)="row">
        <b-button size="sm" @click="row.toggleDetails" class="mr-2">
          {{ row.detailsShowing ? "Hide" : "Show" }} Details
        </b-button>
      </template>

      <template #row-details="row">
        <b-table :items="[row.item]"> </b-table>
      </template>
    </b-table>
    <b-pagination
      v-model="currentPage"
      :total-rows="totalRows"
      :per-page="perPage"
      aria-controls="my-table"
    ></b-pagination>
  </div>
</template>
<script>
export default {
  name: "CarTable",
  props: {
    CarData: Array
  },
  data() {
    return {
      fields: [
        { key: "show_details" },
        { key: "age", label: "Age", sortable: true },
        { key: "gender", label: "Gender", sortable: true },
        { key: "name", label: "Name" },
        { key: "car_make", label: "Car Make", sortable: true }
      ],
      perPage: 10,
      currentPage: 1,
      filter: "",
      totalRows: 1
    };
  },
  mounted() {
    this.totalRows = this.CarData.length;
  },
  methods: {
    onFiltered(filteredItems) {
      this.totalRows = filteredItems.length;
      this.currentPage = 1;
    }
  }
};
</script>
