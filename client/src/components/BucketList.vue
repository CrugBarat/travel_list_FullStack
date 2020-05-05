<template lang="html">
  <div id="favourite_countries">
    <p class="title">Country List</p>
    <div class="country-container">
      <div class="country" v-for="country in bucketList">
        <div><img v-bind:class="visitedClass(country)" :src="country.flag"/></div>
        <p class="name">{{country.name}}</p>
        <button class="button" v-if="!country.visited" v-on:click="updateList(country)">Visited</button>
        <button class="button" v-on:click="deleteCountry(country)">Delete</button>
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
  width: 210px;
  height: 100px;
  opacity: 80%;
  filter: grayscale(80%);
}
.not-visited {
  width: 210px;
  height: 100px;
  opacity: 100%
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
  width: 20.5%;
  margin: 20px;
  float: left;
}
.title {
  font-size: 60px;
  margin-bottom: 30px;
  font-family: 'Audiowide', cursive;
  text-shadow: -1px -1px 0 red, 1px -1px 0 red, -1px 1px 0 red, 1px 1px 0 red;
}
.name {
  font-size: 20px;
}
.button {
  font-size: 15px;
  width: 95px;
}
</style>
