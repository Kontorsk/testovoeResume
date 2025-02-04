<template>
  <form @submit.prevent="submit" class="card card-w30">
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
      <textarea
        v-model="value"
        :placeholder="optionalPlaceholder"
        id="value"
        rows="3"
      />
    </div>

    <button :disabled="activeBtn" class="btn primary">Добавить</button>
  </form>
</template>

<script>
export default {
  emits: ['block-added'],
  data() {
    return {
      value: '',
      type: 'title',
    };
  },
  computed: {
    activeBtn() {
      return this.value.length < 4;
    },
    optionalPlaceholder() {
      if (this.type !== 'avatar') {
        return 'Введите текст (более 4 символов)';
      } else {
        return 'Введите URL';
      }
    },
  },
  methods: {
    submit() {
      this.$emit('block-added', {
        type: this.type,
        value: this.value,
      });
      this.value = '';
      this.type = 'title';
    },
  },
};
</script>
