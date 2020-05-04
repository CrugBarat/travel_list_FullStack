<template lang="html">
  <div id="selected_country">
    <img class="lrg-flag" :src="selectedCountry.flag" />
    <p class="country">{{selectedCountry.name}}</p>
  </div>
</template>

<script>
export default {
  name: 'country-detail',
  props: ['selectedCountry']
}
</script>


<style lang="css" scoped>
#selected_country {
  display: block;
  text-align: center;
  margin: 20px;
  margin-top: 50px;
}
.lrg-flag {
  width: 400px;
  height: 200px;
  opacity: 80%
}
.country {
  font-size: 35px;
  margin-top: 15px;
}

</style>
