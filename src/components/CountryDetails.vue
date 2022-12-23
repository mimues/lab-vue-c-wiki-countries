<template>
    <img :src="`https://flagpedia.net/data/flags/icon/72x54/${country.alpha2Code.toLowerCase()}.png`" alt="country flag"
      style="width: 200px" />
    <h1>{{ country.name.common }}</h1>
    <table class="table">
      <thead></thead>
      <tbody>
        <tr>
          <td style="width: 30%">Capital</td>
          <td>{{ country.capital[0] }}</td>
        </tr>
        <tr>
          <td>Area</td>
          <td>
            {{ country.area }} km <sup>2</sup>
          </td>
        </tr>
        <tr v-if="country.borders.length > 0">
          <td>Borders</td>
          <td>
            <ul class="list-style-none">
              <li v-for="(country, index) in country.borders" :key="index">
                <router-link :to="`/${country}`">
                  {{ country }}
                </router-link>
              </li>
            </ul>
          </td>
        </tr>
      </tbody>
    </table>
</template>
<script>
export default {
  props: {
    country: {
      type: Object,
    }
  },
}
</script>
<style>

</style>