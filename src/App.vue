<template>
  <div id="app">
    <h2>Global population: {{ calculateTotalPopulation }}</h2>

    <label for="country_select">Select a Country:</label>
    <select id="country_select" v-model="selectedCountry">
      <option disabled value="">Select a country</option>
      <option v-for="country in countries" :value="country">{{country.name}}</option>
      </select>
<span v-if="selectedCountry">Flag:<img :src="selectedCountry.flag" alt="avatar" width="20" height="16">Country: {{selectedCountry.name}}</span>







  <!-- Country detail goes here -->

    <button v-on:click="addCountry">Add Country</button>
    <ul>Favourite Countries:<li v-for="country in favouriteCountries" :value="country">
    {{country.name}}<img :src="country.flag" alt="avatar" width="20" height="16"></li></ul>


    <!-- Favourite Countries goes here -->
</div>

</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      countries: [],
      selectedCountry: null,
      favouriteCountries: []
    }
  },
    computed: {
      calculateTotalPopulation(){
        return this.countries.reduce((total, country) => total + country.population, 0)
      },
    },
    mounted(){
      this.fetchCountries()
    },
    methods: {
      fetchCountries(){
        fetch("https://restcountries.eu/rest/v2/all")
        .then(response => response.json())
        .then(data => this.countries = data)
      },
      addCountry(){
        if (this.favouriteCountries.includes(this.selectedCountry)) {
          alert('Pick another country!!!')
        } else {
          return this.favouriteCountries.push(this.selectedCountry);
        }
      }
      // findNeighbouringCountries(){
      //   const array = this.selectedCountry.filter(country => country.borders)
      //   for (code in array) {
      //     if code ===
      //   }
        }
      }
</script>

<style>
.small-flag {
  height: 20px
}



</style>
