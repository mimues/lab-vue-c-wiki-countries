<template>
  <router-link 
    v-for="(country, index) in countries"
    :key="index"
    class="list-group-item list-group-item-action d-flex flex-column justify-content-center align-items-center"
    :to="`/${country.alpha3Code}`"
  >
    <img :src="`https://flagpedia.net/data/flags/icon/72x54/${country.alpha2Code.toLowerCase()}.png`" width="75" />
    <p class="m-0">{{ country.name.common }}</p>
  </router-link>
</template>
<script>
export default {
  props: {
    countries: {
      type: Array,
    }
  }
}
</script>
<style>

</style>