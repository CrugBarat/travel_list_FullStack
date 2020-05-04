<template>
  <div id="app">
    <p class="title">Travel List</p>
    <country-select :countries="countries"/>
    <country-detail v-if="selectedCountry" :selectedCountry="selectedCountry">
    </country-detail>
    <div class="button-container">
      <button v-if="!bucketList.includes(selectedCountry) && selectedCountry" v-on:click="addToBucketList">Add Country</button>
      <button v-on:click="viewList">View List</button>
      <button v-on:click="clearList">Clear List</button>
    </div>
    <bucket-list v-if="listSelected" :bucketList="bucketList"></bucket-list>
  </div>
</template>

<script>
import CountryDetail from '@/components/CountryDetail.vue';
import BucketList from '@/components/BucketList.vue';
import CountrySelect from '@/components/CountrySelect';
import BucketService from '@/services/BucketService';
import {eventBus} from '@/main.js';

export default {
  name: 'App',
  data() {
    return {
      countries: [],
      selectedCountry: null,
      bucketList: [],
      listSelected: null
    }
  },
  components: {
    'country-detail': CountryDetail,
    'bucket-list': BucketList,
    'country-select': CountrySelect
  },
  mounted(){
    this.getCountries();
    this.getBucketList();

    eventBus.$on('country-selected', (country) => {
      this.selectedCountry = country;
    })

    eventBus.$on('country-deleted', (deletedCountry) => {
      let index = this.bucketList.findIndex(country => country._id === deletedCountry._id)
      this.bucketList.splice(index, 1)
    })

    eventBus.$on('country-updated', (updatedCountry) => {
      let index = this.bucketList.findIndex(country => country._id === updatedCountry._id)
      this.bucketList.splice(index, 1, updatedCountry)
    })
  },
  methods: {
    getCountries(){
      fetch("https://restcountries.eu/rest/v2/all")
      .then(res => res.json())
      .then(countries => this.countries = countries)
    },
    getBucketList(){
      BucketService.getBucketList()
      .then(bucketList => this.bucketList = bucketList)
    },
    addToBucketList(event){
      BucketService.addCountry(this.selectedCountry)
      .then(country => this.bucketList.push(country));
    },
    viewList(){
      this.listSelected = true;
    },
    clearList(){
      BucketService.deleteAll()
      .then(() => this.bucketList = [])
    }
  }
}
</script>

<style lang="css" scoped>
p{
  margin: 0;
  padding: 0;
}
.title {
  font-size: 10vw;
  text-align: center;
}
.button-container {
  display: block;
  text-align: center;
}

</style>

<style>
body {
  background-image: url('assets/background.jpg');
  background-size: cover;
  background-attachment: fixed;
  background-position: center;
  color: white;
}
p {
  margin: 0;
  padding: 0;
}
</style>
