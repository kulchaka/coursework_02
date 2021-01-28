<template>
  <div class="container column">
    <form class="card card-w30">
      <form-options title="Тип блока" :options="options"></form-options>
      <form-text title="Значение" v-model="inputText"></form-text>
      <app-button text="добавить" :disabled="disabledBtn" color="primary"></app-button>
    </form>

    <div class="card card-w70">
      <h1>Резюме Nickname</h1>
      <div class="avatar">
        <img src="https://cdn.dribbble.com/users/5592443/screenshots/14279501/drbl_pop_r_m_rick_4x.png">
      </div>
      <h2>Опыт работы</h2>
      <p>
        главный герой американского мультсериала «Рик и Морти», гениальный учёный, изобретатель, атеист (хотя в некоторых сериях он даже молится Богу, однако, каждый раз после чудесного спасения ссылается на удачу и вновь отвергает его существование), алкоголик, социопат, дедушка Морти. На момент начала третьего сезона ему 70 лет[1]. Рик боится пиратов, а его главной слабостью является некий - "Санчезиум". Исходя из того, что существует неограниченное количество вселенных, существует неограниченное количество Риков, герой сериала предположительно принадлежит к измерению С-137. В серии комикcов Рик относится к измерению C-132, а в игре «Pocket Mortys» — к измерению C-123[2]. Прототипом Рика Санчеза является Эмметт Браун, герой кинотрилогии «Назад в будущее»[3].
      </p>
      <h3>Добавьте первый блок, чтобы увидеть результат</h3>
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
    <div class="loader"></div>
  </div>
</template>

<script>

import FormOptions from './components/FormOptions'
import FormText from './components/FormText'
import AppButton from './components/AppButton'

export default {
  data () {
    return {
      inputText: '',
      options: [
        { value: 'title', title: 'Заголовок' },
        { value: 'subtitle', title: 'Подзаголовок' },
        { value: 'avatar', title: 'Аватар' },
        { value: 'text', title: 'Текст' }
      ]
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
  components: { FormOptions, FormText, AppButton }
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
