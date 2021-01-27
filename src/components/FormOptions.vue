<template>
  <div class="form-control">
    <label for="type">{{ title }}</label>
      <select id="type">
        <option v-for="(item, index) in options" :key="index" :value="item.value">{{ item.title }}</option>
      </select>
  </div>
</template>
<script>
export default {
  props: {
    title: String,
    options: Array
  }
}
</script>
<style>

</style>
