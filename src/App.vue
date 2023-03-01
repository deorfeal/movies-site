<script>

import Main from './Main.vue'
// import Search from './Search.vue'

export default {
  name: 'App',
  components: {
    Main,
    // Search
  },
  data() {
    return {
    }
  },

}

</script>

<template>
  <div class="biggest-wrapper" id="biggest-wrapper">
    <Main />
    <!-- <Search/> -->
  </div>
</template>

<style lang="scss">
@import './assets/scss/style.scss';
</style>