<template>
  <ul class="list" v-for="(item, index) in comments" :key="index">
        <li class="list-item">
          <div>
            <p><strong>{{ item.email }}</strong></p>
            <small>{{ item.text }}</small>
          </div>
        </li>
  </ul>
</template>
<script>
export default {
  props: {
    comments: Array
  }
}
</script>
<style>

</style>
