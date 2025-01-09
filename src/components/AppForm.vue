<template>
    <form class="card card-w30" @submit.prevent="submit">
      <div class="form-control">
        <label for="type">Тип блока</label>
        <select id="type" v-model="type">
          <option value="title">Заголовок</option>
          <option value="subtitle">Подзаголовок</option>
          <option value="avatar">Аватар</option>
          <option value="text">Текст</option>
        </select>
      </div>

      <div class="form-control">
        <label for="value">Значение</label>
        <!-- нет слота - делай самозакрывающий -->
        <textarea id="value" rows="3" v-model="value"></textarea>
      </div>

      <button class="btn primary" :disabled="activeBtn">Добавить</button>
    </form>
</template>

<script>
export default {
  emits: ['block-added'],
  data () {
    return {
      value: '',
      type: 'title'
    }
  },
  computed: {
    activeBtn () {
      return this.value.length < 4 // это даже не формат, это пиздец
    }
  },
  methods: {
    submit () {
      // ошибка
      // this.$emit('block-added', {
      //   type: this.type,
      //   value: this.value,
      //   // id: Date.now() - зачем?
      // }),
      this.value = ''
      this.type = 'title'
    }
  }
}
</script>
<!-- юзлесс тег, тк пустой - сноси -->
<style scoped>

</style>
