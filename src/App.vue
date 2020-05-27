<template>
  <div class="container">
    <div class="row">
      <div class="col-sm-12">
        <navHeader @pageWasChanged="currentPage = $event"></navHeader>
        <keep-alive>
          <component :is="currentPage"></component>
        </keep-alive>
      </div>
    </div>
  </div>
</template>

<script>
import Header from './components/Header.vue';
import CardFront from './components/card/CardFront.vue'
import CardInsideLeft from './components/card/CardInsideLeft.vue'
import CardInsideRight from './components/card/CardInsideRight.vue'
import CardBack from './components/card/CardBack.vue'

export default {
  data: function() {
    return {
      currentPage: 'cardFront'
    }
  },
  components: {
    navHeader: Header,
    cardFront: CardFront,
    CardInsideLeft: CardInsideLeft,
    CardInsideRight: CardInsideRight,
    CardBack: CardBack
  }
}
</script>

<style>
  body {
    font-family: Verdana, Geneva, Tahoma, sans-serif;
    color: #333; 
  }
</style>
