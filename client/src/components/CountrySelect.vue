<template lang="html">
  <div class="select-container">
    <div class="select">
      <select id="country_select" v-on:change="countrySelected" v-model="selectedCountry">
        <option disabled>Select A Country</option>
        <option v-for="country in countries" :value="country">{{country.name}}</option>
      </select>
    </div>
  </div>
</template>

<script>
import {eventBus} from '@/main.js';

export default {
  name: 'country-select',
  props: ['countries'],
  data() {
    return {
      selectedCountry: null
    }
  },
  methods: {
    countrySelected(){
      eventBus.$emit('country-selected', this.selectedCountry)
    }
  }
}
</script>

<style lang="css" scoped>
.select-container {
  display: block;
  text-align: center;
}
.select {
  margin: 20px;
}
select {
  color: white;
  background-color: transparent;
  height: 30px;
  font-size: 20px;
  font-family: 'Open Sans', sans-serif;
}
</style>
