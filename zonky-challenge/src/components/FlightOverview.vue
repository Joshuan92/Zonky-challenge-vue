<template>
  <div>
    <h1>Flights</h1>
        <b-table striped hover :items="flights" :fields="['cityFrom', 'cityTo', 'price', ]">
            <template v-slot:cell(name)="data">
             <!-- <router-link :to="`/pet/${species}/${data.index}`">{{ data.value }}</router-link> -->
            </template>
        </b-table>
  </div>
</template>

<script>
export default {
    props: {
        flights: Object
    }
}
</script>
