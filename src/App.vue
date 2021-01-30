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

    <div class="card card-w70">
      <template v-for="(item, index) in arrBlocks" :key="index">

        <header-block :title="item.text" v-if="item.tag === 'h1'"></header-block>

        <subtitle-block :title="item.text" v-if="item.tag === 'h2'"></subtitle-block>

        <avatar-block :link="item.text" v-if="item.tag === 'src'"></avatar-block>

        <text-block :title="item.text" v-if="item.tag === 'p'"></text-block>

      </template>
      <h3 v-if="!arrBlocks.length">Добавьте первый блок, чтобы увидеть результат</h3>
    </div>
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
import HeaderBlock from './components/HeaderBlock'
import SubtitleBlock from './components/SubtitleBlock'
import AvatarBlock from './components/AvatarBlock'
import TextBlock from './components/TextBlock'
import ListComments from './components/ListComments'
import axios from 'axios'

export default {
  data () {
    return {
      inputText: '',
      selected: 'h1',
      arrOptions: [
        { tag: 'h1', value: 'Заголовок' },
        { tag: 'h2', value: 'Подзаголовок' },
        { tag: 'src', value: 'Аватар' },
        { tag: 'p', value: 'Текст' }
      ],
      arrBlocks: [],
      arrComments: [],
      loader: false
    }
  },
  methods: {
    formSub () {
      this.arrBlocks.push({ tag: `${this.selected}`, text: `${this.inputText} ` })
      this.selected = 'h1'
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
  components: { FormOptions, FormText, AppButton, HeaderBlock, SubtitleBlock, AvatarBlock, TextBlock, ListComments }
}
</script>

<style>
</style>
