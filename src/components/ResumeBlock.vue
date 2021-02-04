<template>
  <div class="card card-w70">
    <template v-if="blocks.length">
      <component
        v-for="(item, index) in blocks" :key="index"
        :is="'resume-' + item.tag"
        v-bind="{value: item.text}"
      ></component>
    </template>
    <h3 v-else>Добавьте первый блок, чтобы увидеть результат</h3>
  </div>
</template>
<script>

import ResumeTitle from './tagcomponents/ResumeTitle'
import ResumeSubtitle from './tagcomponents/ResumeSubtitle'
import ResumeImglink from './tagcomponents/ResumeImglink'
import ResumeText from './tagcomponents/ResumeText'

export default {
  props: ['blocks'],
  components: { ResumeTitle, ResumeSubtitle, ResumeImglink, ResumeText }
}
</script>
<style>

</style>
