<template>
  <div @mouseover="showOptions = true" @mouseleave="showOptions = false">
    <transition name="fade">
      <form class="small" v-show="showOptions">
        <label for="selectBox">Font size</label>
        <select class="custom-select custom-select-inline" v-model="setFontSize">
          <option value="42">42px</option>
          <option value="48">48px</option>
          <option value="56">56px</option>
          <option value="64">64px</option>
        </select>
        <div class="form-check form-check-inline">
          <label for class="form-check-label">
            <input type="radio" class="form-check-input" value="left" v-model="setTextAlign" /> Left
          </label>
        </div>
        <div class="form-check form-check-inline">
          <label for class="form-check-label">
            <input type="radio" class="form-check-input" value="center" v-model="setTextAlign" /> Center
          </label>
        </div>
        <div class="form-check form-check-inline">
          <label for class="form-check-label">
            <input type="radio" class="form-check-input" value="right" v-model="setTextAlign" /> Right
          </label>
        </div>
        <div class="form-check form-check-inline">
          <label class="form-check-label">
            <input type="checkbox" class="form-check-input" v-model="setTextBold" /> Bold
          </label>
        </div>
        <div class="form-check form-check-inline">
          <label class="form-check-label">
            <input type="checkbox" class="form-check-input" v-model="setTextItalic" /> Italic
          </label>
        </div>
      </form>
    </transition>
    <p :style="styleObject" :class="{ bold: setTextBold, italic: setTextItalic }">{{ displayText }}</p>
  </div>
</template>

<script>
export default {
  props: {
    displayText: [String],
    containerHeight: {
      type: Number,
      default: 200
    }
  },
  data: function() {
    return {
      showOptions: false,
      setFontSize: "",
      setTextAlign: "",
      setTextBold: false,
      setTextItalic: false
    };
  },
  computed: {
    styleObject: function() {
      return {
        height: this.containerHeight + "px",
        fontSize: this.setFontSize + "px",
        textAlign: this.setTextAlign
      };
    }
  }
};
</script>

<style scoped>
p {
  font-family: "Tangerine", cursive;
  font-size: 42px;
  line-height: 42px;
  text-shadow: 2px 2px 2px #aaa;
  color: #4d4d4d;
  margin: 5px 0;
  border: 1px dotted grey;
  /* Preserves line breaks */
  white-space: pre-line;
  overflow: hidden;
}

.bold {
  font-weight: bold;
}

.italic {
  font-style: italic;
}

form {
  position: absolute;
  border-bottom: 1px dotted grey;
  margin-top: 10px;
  margin-bottom: 5px;
  padding-bottom: 5px;
}

select {
  height: 40%;
}

.custom-select {
  width: unset;
}
</style>