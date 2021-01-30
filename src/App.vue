<template>
  <div class="container column">
    <form class="card card-w30" @submit.prevent="formSub">
      <form-options
        title="Тип блока"
        :options="options"
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
      <template v-for="(item, index) in arrBlock" :key="index">

        <header-block :title="item.text" v-if="item.tag === 'h1'"></header-block>

        <subtitle-block :title="item.text" v-if="item.tag === 'h2'"></subtitle-block>

        <avatar-block :link="item.text" v-if="item.tag === 'src'"></avatar-block>

        <text-block :title="item.text" v-if="item.tag === 'p'"></text-block>
      </template>
      <h3 v-if="!arrBlock.length">Добавьте первый блок, чтобы увидеть результат</h3>
    </div>
  </div>
  <div class="container">
    <p>
      <button class="btn primary">Загрузить комментарии</button>
    </p>
    <div class="card">
      <h2>Комментарии</h2>
      <ul class="list">
        <li class="list-item">
          <div>
            <p><strong>test@microsoft.com</strong></p>
            <small>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Eligendi, reiciendis.</small>
          </div>
        </li>
      </ul>
    </div>
    <!-- <div class="loader"></div> -->
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

export default {
  data () {
    return {
      inputText: '',
      selected: 'h1',
      // options: [
      //   { tag: 'h1', title: 'Заголовок' },
      //   { tag: 'h2', title: 'Подзаголовок' },
      //   { tag: 'src', title: 'Аватар' },
      //   { tag: 'p', title: 'Текст' }
      // ],
      options: {
        h1: 'Заголовок',
        h2: 'Подзаголовок',
        src: 'Аватар',
        p: 'Текст'
      },
      arrBlock: []
    }
  },
  methods: {
    formSub () {
      this.arrBlock.push({ tag: `${this.selected}`, text: `${this.inputText} ` })
      this.selected = 'h1'
      this.inputText = ''
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
  components: { FormOptions, FormText, AppButton, HeaderBlock, SubtitleBlock, AvatarBlock, TextBlock }
}
</script>

<style>
  .avatar {
    display: flex;
    justify-content: center;
  }

  .avatar img {
    width: 150px;
    height: auto;
    border-radius: 50%;
  }
</style>
