<template lang="html">
  <div id="favourite_countries">
    <h2>Bucket List</h2>
    <ul>
      <li  v-for="country in bucketList" v-bind:class="visitedClass(country )">{{country.name}} <img class="small-flag" :src="country.flag"/> <button v-if="!country.visited" v-on:click="updateList(country)">Visit!</button></li>
    </ul>
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
</style>
