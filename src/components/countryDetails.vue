<template lang="html">
  <div v-if="country">
    <p>Name: {{country.name}}</p>
    <p>Capital: {{country.capital}}</p>
    <p>Population: {{country.population}}</p>
  </div>
</template>

<script>

export default {
  name: "country-details",
  props: ['country']
}
</script>

<style lang="css" scoped>
</style>
