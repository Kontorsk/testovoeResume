<template>
  <div v-if="alert" :class="alert.type" class="alert">
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
      required: true,
      validator(value) {
        return ['danger', 'primary'].includes(value.type);
      },
    },
  },
  emits: ['close'],
};
</script>
