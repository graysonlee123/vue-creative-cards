<template>
  <textarea></textarea>
</template>

<script>
new Vue({
  data: function() {
    return {
      textValue: 'Type here'
    }
  },
  methods: {
    changeText: function() {
      this.textValue = 'Text changed'
    }
  },
})
</script>

<style>
</style>