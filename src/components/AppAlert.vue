<template>
  <div class="alert" v-if="alert" :class="alert.type">
    <h3>{{ alert.title }}</h3>
    <p>{{ alert.text }}</p>
    <button class="btn" :class="alert.type" @click="$emit('close')">
      Закрыть
    </button>
  </div>
</template>

<script>
export default {
  props: {
    alert: {
      type: Object,
      default: null,
      validator(value) {
        return ['danger', 'primary'].includes(value.type);
      },
    },
  },
  emits: ['close'],
};
</script>
