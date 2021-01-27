<template>
  <button class="btn" :class="color">{{ text }}</button>
</template>
<script>
export default {
  props: {
    text: String,
    color: {
      type: String,
      default: '',
      validator (value) {
        return ['', 'primary', 'danger'].includes(value)
      }
    }
  }
}
</script>
<style>

</style>
