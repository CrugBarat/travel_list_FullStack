<template lang="html">
  <div id="favourite_countries">
    <p class="title">Country List</p>
    <div class="country-container">
      <country-item v-for="country in bucketList" :country="country"></country-item>
    </div>
  </div>
</template>

<script>
import CountryItem from '@/components/CountryItem.vue';

export default {
  name: 'bucket-list',
  props: ['bucketList'],
  components: {
    'country-item': CountryItem
  },
}
</script>

<style lang="css" scoped>
#favourite_countries {
  display: block;
  text-align: center;
  margin-top: 60px;
}
.country-container {
  display: inline-block;
  width: 80%;
}
.title {
  font-size: 60px;
  margin-bottom: 30px;
  font-family: 'Audiowide', cursive;
  text-shadow: -1px -1px 0 red, 1px -1px 0 red, -1px 1px 0 red, 1px 1px 0 red;
}
</style>
