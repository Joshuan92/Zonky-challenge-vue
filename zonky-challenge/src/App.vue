<template>
  <div id="app">
    <NavBar />
    <FlightsOverview v-if="fetchedFlightsData.length" :flights="flightsData" />
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
      fetchedFlightsData: {},
      flightsData: []
    };
  },
  // computed: {
  //   averagePrice() {

  //   }
  // },
  methods: {},
  mounted() {
    fetch(
      "https://api.skypicker.com/flights?fly_from=PRG&fly_to=ZRH&partner=picky",
      {
        method: "get",
        headers: { "Content-Type": "application/json" }
      }
    )
      .then(response => {
        return response.json();
      })

      .then(jsonData => {
        this.fetchedFlightsData = jsonData.data;
      })
      .then(() => {
        this.fetchedFlightsData.forEach(flight => {
          this.flightsData.push({
            from: flight.cityFrom + ", " + flight.countryFrom.name,
            "time of departure": new Date(
              flight.dTime * 1000
            ).toLocaleTimeString(),
            "date of departure": new Date(
              flight.dTime * 1000
            ).toLocaleDateString(),
            to: flight.cityTo + ", " + flight.countryTo.name,
            "time of arrival": new Date(
              flight.aTime * 1000
            ).toLocaleTimeString(),
            "date of arrival": new Date(
              flight.aTime * 1000
            ).toLocaleDateString(),
            price: flight.price + " EUR"
          });
        });
      });
  }
};
</script>
