<template>
  <div class="form-control">
    <label for="value">{{ title }}</label>
    <textarea id="value" rows="3"></textarea>
  </div>
</template>
<script>
export default {
  props: {
    title: String
  }
}
</script>
<style>

</style>
