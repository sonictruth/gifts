<script>
  import 'animate.css';

  import GiftHeader from './components/GiftHeader';
  import GiftList from './components/GiftList';
  import './assets/fonts/EngraversGothic-font.css';
  import './css/minimal-bootstrap.css';
  import './css/base.css';


  export default {
    methods: {
      applyFilters(newFilters) {
        this.$refs['gift-list'].filters = newFilters;
      },
    },
    components: {
      GiftHeader,
      GiftList,
    },
  };
</script>

<template>
  <div id="app" v-cloak>
   <gift-header v-on:filtersChanged="applyFilters" />
   <gift-list ref="gift-list" />
  </div>
</template>
