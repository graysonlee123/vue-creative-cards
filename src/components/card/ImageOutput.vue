<template>
  <div
    class="image-container"
    :style="styleObject"
    @mouseover="showOptions = true"
    @mouseleave="showOptions = false"
  >
    <transition name="scale">
      <button
        type="button"
        class="btn btn-outline-danger btn-sm"
        v-show="showOptions"
        @click="clearImageProp"
      >Remove image</button>
    </transition>
    <img id="outputImage" :src="displayImage" :alt="displayImage" />
  </div>
</template>

<script>
import Firebase from "firebase";

export default {
  props: {
    displayImage: {
      type: String
    },
    containerHeight: {
      type: Number,
      default: 200
    },
    clearImageProp: {
      type: Function
    }
  },
  data: function() {
    return {
      showOptions: false
    };
  },
  watch: {
    displayImage: function() {
      const storageRef = Firebase.storage().ref(
        "user_uploads/" + this.displayImage
      );
      storageRef.getDownloadURL().then(function(data) {
        const image = document.getElementById("outputImage");
        image.src = data;
      });
    }
  },
  computed: {
    styleObject: function() {
      return {
        height: this.containerHeight + "px"
      };
    }
  }
};
</script>

<style scoped>
.image-container {
  border: 1px dotted grey;
  overflow: hidden;
  margin: 5px 0;
}

button {
  position: absolute;
  z-index: 1;
}

img {
  width: 130%;
}

.scale-enter-active {
  animation: scale-in 0.5s;
}

.scale-leave-active {
  animation: scale-out 0.5s;
}

@keyframes scale-in {
  from {
    transform: scale(0);
  }
  to {
    transform: scale(1);
  }
}

@keyframes scale-out {
  from {
    transform: scale(1);
  }
  to {
    transform: scale(0);
  }
}
</style>