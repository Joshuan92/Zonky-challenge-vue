<template>
  <div>
    <h1 class="m-3">Top {{perPage*currentPage}} cheapest flights</h1>
    <h3 class="m-1">from {{fetchedFlightsData[0].cityFrom}} to {{fetchedFlightsData[0].cityTo}} </h3>
    <b-table id="flightsTable" striped hover responsive :items="flights" :perPage="perPage" :current-page="currentPage">
      <template v-slot:cell(name)="data">
        <!-- <router-link :to="`/pet/${species}/${data.index}`">{{ data.value }}</router-link> -->
      </template>
    </b-table>
    <b-pagination
      v-model="currentPage"
      :total-rows="flights.length"
      :per-page="perPage"
      align="center"
      aria-controls="flightsTable"
      small
    ></b-pagination>
  </div>
</template>

<script>
export default {
    data() {
        return {
            perPage: 5,
            currentPage: 1,
            totalRows: this.calculatedData.numberOfFligts
        }
    },
  props: {
    flights: Array,
    calculatedData: Object,
    fetchedFlightsData: Array
  }
};
</script>
