<template>
  <div class="container">
    <div class="row">
      <div class="col-sm-12">
        <nav-header></nav-header>
        <card-front></card-front>
      </div>
    </div>
  </div>
</template>

<script>
import Header from './components/Header.vue';
import CardFront from './components/card/CardFront.vue'

export default {
  components: {
    'nav-header': Header,
    'card-front': CardFront
  }
}
</script>

<style>
  body {
    font-family: Verdana, Geneva, Tahoma, sans-serif;
    color: #333; 
  }
</style>
