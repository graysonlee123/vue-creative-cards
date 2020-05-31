<template>
  <div class="container">
    <div class="row">
      <div class="col-sm-12">
        <navHeader @pageWasChanged="currentPage = $event"></navHeader>
        <keep-alive>
          <component :is="currentPage"></component>
        </keep-alive>
        <cc-footer>
          <p class="text-center" slot="app-name">&copy; Creative Cards</p>
          <nav>
            <ul class="nav justify-content-center">
              <li class="nav-item">
                <a href="#" class="nav-link">Home</a>
              </li>
              <li class="nav-item">
                <a href="#" class="nav-link">About Us</a>
              </li>
              <li class="nav-item">
                <a href="#" class="nav-link">Contact</a>
              </li>
            </ul>
          </nav>
        </cc-footer>
      </div>
    </div>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";
import CardFront from "./components/card/CardFront.vue";
import CardInsideLeft from "./components/card/CardInsideLeft.vue";
import CardInsideRight from "./components/card/CardInsideRight.vue";
import CardBack from "./components/card/CardBack.vue";

import FirebaseConfig from "../firebaseConfig.js";
console.log(FirebaseConfig);

export default {
  data: function() {
    return {
      currentPage: "cardFront"
    };
  },
  components: {
    navHeader: Header,
    cardFront: CardFront,
    CardInsideLeft: CardInsideLeft,
    CardInsideRight: CardInsideRight,
    CardBack: CardBack,
    ccFooter: Footer
  }
};
</script>

<style>
body {
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  color: #333;
}

.fade-enter, .fade-leave-to {
  opacity: 0;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
</style>
