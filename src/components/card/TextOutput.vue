<template>
  <div>
    <p>{{ displayText }}</p>
  </div>
</template>

<script>
export default {
  props: ['displayText'],
  data: function() {
    return {
      text: 'test'
    }
  }
}
</script>

<style>

</style>