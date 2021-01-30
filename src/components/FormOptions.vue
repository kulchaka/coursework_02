<template>
  <div class="form-control">
    <label for="type">{{ title }}</label>
      <select :value="modelValue" @change="change">
        <option v-for="(item, index) in options" :key="index" :value="item.tag">{{ item.value }}</option>
      </select>
  </div>
</template>
<script>
export default {
  emits: ['update:modelValue'],
  props: {
    modelValue: String,
    title: String,
    options: Array
  },
  methods: {
    change (event) {
      this.$emit('update:modelValue', event.target.value)
    }
  }
}
</script>
<style>

</style>
