<template>
  <div class="container column">
    <form class="card card-w30" @submit.prevent="formSub">
      <form-options
        title="Тип блока"
        :options="arrOptions"
        v-model="selected"
      ></form-options>
      <form-text title="Значение" v-model.trim="inputText"></form-text>
        <app-button
          text="добавить"
          :disabled="disabledBtn"
          color="primary"
        ></app-button>
    </form>

    <resume-block :blocks="arrBlocks"></resume-block>

  </div>
  <div class="container">
    <p>
      <app-button
          text="Загрузить комментарии"
          color="primary"
          @click="renderComments"
        ></app-button>
    </p>
    <div class="card">
      <subtitle-block title="Комментарии"></subtitle-block>
      <list-comments
        :comments="arrComments"
        v-if="arrComments.length"
      ></list-comments>
    </div>
    <div class="loader" v-if="loader === true"></div>
  </div>
</template>

<script>

import FormOptions from './components/FormOptions'
import FormText from './components/FormText'
import AppButton from './components/AppButton'
import SubtitleBlock from './components/SubtitleBlock'
import ListComments from './components/ListComments'
import ResumeBlock from './components/ResumeBlock'
import axios from 'axios'

export default {
  data () {
    return {
      inputText: '',
      selected: 'title',
      arrOptions: [
        { tag: 'title', value: 'Заголовок' },
        { tag: 'subtitle', value: 'Подзаголовок' },
        { tag: 'imglink', value: 'Аватар' },
        { tag: 'text', value: 'Текст' }
      ],
      arrBlocks: [],
      arrComments: [],
      loader: false
    }
  },
  methods: {
    formSub () {
      this.arrBlocks.push({ tag: `${this.selected}`, text: `${this.inputText} ` })
      this.selected = 'title'
      this.inputText = ''
    },
    async renderComments () {
      this.loader = true
      try {
        const { data } = await axios.get('https://jsonplaceholder.typicode.com/comments?_limit=42')
        if (!data) {
          throw new Error('the list is empty')
        }
        const res = Object.keys(data).map(key => {
          return {
            email: data[key].email,
            text: data[key].body
          }
        })
        this.loader = false
        this.arrComments = res
      } catch (error) {
        this.loader = true
        console.log(error.message)
      }
    }
  },
  computed: {
    disabledBtn () {
      if (this.inputText.length < 3) {
        return true
      }
      return false
    }
  },
  components: { FormOptions, FormText, AppButton, SubtitleBlock, ListComments, ResumeBlock }
}
</script>

<style>
</style>
