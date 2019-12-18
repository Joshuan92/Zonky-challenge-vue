<template>
  <div id="app">
    <NavBar />
    <FlightsOverview
      v-if="fetchedFlightsData.length"
      :fetchedFlightsData="fetchedFlightsData"
      :flights="flightsData"
      :calculatedData="calculatedData"
    />
    <div v-else class="text-center m-3">
      <b-spinner variant="primary" label="Text Centered"></b-spinner>
      <br />
      Loading data. You will get your cheapest flights in a second.
    </div>
    <router-view />
  </div>
</template>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>

<script>
import NavBar from "./components/NavBar.vue";
import FlightsOverview from "./components/FlightOverview.vue";

export default {
  name: "app",
  components: {
    NavBar,
    FlightsOverview
  },
  data() {
    return {
      apiURL:
        "https://api.skypicker.com/flights?fly_from=PRG&fly_to=ZRH&partner=picky",
      fetchedFlightsData: {},
      flightsData: [],
      calculatedData: {
        totalPrice: null,
        averagePrice: null,
        numberOfFlights: null
      }
    };
  },
  methods: {},
  mounted() {
    fetch(this.apiURL, {
      method: "get",
      headers: { "Content-Type": "application/json" }
    })
      .then(response => {
        return response.json();
      })

      .then(jsonData => {
        this.fetchedFlightsData = jsonData.data;
      })
      .then(() => {
        this.fetchedFlightsData.forEach(flight => {
          this.calculatedData.totalPrice += flight.price;
          this.flightsData.push({
            from: flight.cityFrom + ", " + flight.countryFrom.name,
            "date and time of departure":
              new Date(flight.dTime * 1000).toLocaleTimeString() +
              ", " +
              new Date(flight.dTime * 1000).toLocaleDateString(),
            to: flight.cityTo + ", " + flight.countryTo.name,
            "time of arrival":
              new Date(flight.aTime * 1000).toLocaleTimeString() +
              ", " +
              new Date(flight.aTime * 1000).toLocaleDateString(),
            "number of flights": flight.pnr_count,
            "flight duration": flight.fly_duration,
            price: flight.price + " EUR"
          });
        });
      })
      .then(() => {
        this.calculatedData.averagePrice =
          this.calculatedData.totalPrice / this.flightsData.length;
        this.calculatedData.numberOfFlights = this.flightsData.length;
      });
  }
};
</script>
