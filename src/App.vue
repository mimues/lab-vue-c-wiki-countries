<template>
  <div class="app">
    <Navbar />
    <!-- Bootstrap container wrapper div -->
    <div class="container">
        <h1 v-if="!countries.length">Loading countries</h1>
        <div v-else class="row">
          <!-- Countries List (Bootstrap column) -->
          <div class="col-5" style="max-height: 90vh; overflow: scroll">
            <div class="list-group">
              <CountriesList :countries="countries" @selected-country="selectedCountryHandler" />
            </div>
          </div>

          <!-- Country Details (Bootstrap column) -->
          <div class="col-7" v-if="selectedCountry.alpha3Code">
          <!-- <router-link v-if="selectedCountry.alpha3Code" :to="`/${selectedCountry.alpha3Code}`"> -->
            <CountryDetails :country="selectedCountry" :key="$route.params.alpha3Code"/>
          </div>
        </div>
      </div>

  </div>
</template>

<script>
import Navbar from './components/Navbar.vue';
import CountriesList from './components/CountriesList.vue';
import CountryDetails from './components/CountryDetails.vue';

export default {
  components: {
    Navbar,
    CountriesList,
    CountryDetails
  },
  data() {
    return {
      countries: [],
      selectedCountry: {}
    }
  },
  async mounted() {
    const response = await fetch("https://ih-countries-api.herokuapp.com/countries")
    const data = await response.json()
    console.log(data)
    this.countries = data
  },
  methods: {
    selectedCountryHandler(country) {
      this.selectedCountry = country
    }
  },
  watch: {
    '$route.params.alpha3Code'() {
      console.log("HOLA???")
      if (this.$route.params.alpha3Code) {
        const selectedCountry = this.countries.find(country => country.alpha3Code === this.$route.params.alpha3Code)
        console.log('HOLA?',selectedCountry)
        this.selectedCountry = selectedCountry
      }
    }
  }
}

</script>

<style>

</style>