<template lang="html">
  <div class="country">
    <div><img v-bind:class="visitedClass()" :src="country.flag"/></div>
    <p class="name">{{country.name}}</p>
    <button class="button" v-if="!country.visited" v-on:click="updateList">Visited</button>
    <button class="button" v-on:click="deleteCountry">Delete</button>
  </div>
</template>

<script>
import BucketService from '@/services/BucketService.js';
import {eventBus} from '@/main.js';

export default {
  name: 'country-item',
  props:['country'],
  methods: {
    updateList(){
      const updatedVisit = {visited: true}
      BucketService.updateCountry(this.country._id, updatedVisit)
      .then((country) => eventBus.$emit('country-updated', country))
    },
    deleteCountry(){
      BucketService.deleteCountry(this.country._id)
      .then(() => eventBus.$emit('country-deleted', this.country._id))
    },
    visitedClass() {
      return this.country.visited ? "visited" : "not-visited";
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
.country {
  color: white;
  width: 20.5%;
  margin: 20px;
  float: left;
}
.name {
  font-size: 20px;
}
.button {
  font-size: 15px;
  width: 95px;
}
</style>
