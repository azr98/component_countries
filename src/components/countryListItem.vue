<template lang="html">
  <div v-if="country">
    <li v-on:click="handleClick">{{country.name}}</li>
  </div>
</template>

<script>

import {eventBus} from "../main.js";

export default {
  name: "country-list-item",
  props: ['country'],
  methods: {
    handleClick(){
      eventBus.$emit('select-country', this.country);
    }
  }
}
</script>

<style lang="css" scoped>
</style>
