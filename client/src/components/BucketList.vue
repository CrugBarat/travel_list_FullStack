<template lang="html">
  <div id="favourite_countries">
    <p class="title">Country List</p>
    <div class="country-container">
      <div class="country" v-for="country in bucketList">
        <div class=""><img class="flag" :src="country.flag"/></div>
        <div v-bind:class="visitedClass(country)">{{country.name}}</div>
        <button v-if="!country.visited" v-on:click="updateList(country)">Visited</button>
        <button v-on:click="deleteCountry(country)">Delete</button>
      </div>
    </div>
  </div>
</template>

<script>
import BucketService from '@/services/BucketService.js';
import {eventBus} from '@/main.js';

export default {
  name: 'bucket-list',
  props: ['bucketList'],
  methods: {
    updateList(country){
      const updatedVisit = {visited: true}
      BucketService.updateCountry(country._id, updatedVisit)
      .then((country) => eventBus.$emit('country-updated', country))
    },
    deleteCountry(country){
      BucketService.deleteCountry(country._id)
      .then((country) => eventBus.$emit('country-deleted', country))
    },
    visitedClass(country) {
      return country.visited ? "visited" : "not-visited"
    }
  }
}
</script>

<style lang="css" scoped>
.visited {
  color: green;
}
.not-visited {
  color: red;
}
#favourite_countries {
  display: block;
  text-align: center;
  margin-top: 60px;
}
.country-container {
  display: inline-block;
  width: 80%;
}
.country {
  color: white;
  width: 19%;
  margin: 20px;
  float: left;
}
.flag {
  width: 130px;
  height: 65px;
  opacity: 80%
}
.title {
  font-size: 60px;
  margin-bottom: 30px;
}

</style>
