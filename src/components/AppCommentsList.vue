<template>
  <div>
    <!-- тут "p" используется для отступа - пиздец, сделай отдельный компонент для этой кнопки с 1м классом, который будет делать то же самое, что и "p" -->
     <!-- btn и primary, здесь его просто вызови и повесь событие -->
    <p>
      <button class="btn primary" @click="$emit('load')">Загрузить комментарии</button>
    </p>
    <div class="card" v-if="wasLoaded">
      <h2>Комментарии</h2>
      <ul class="list">
        <!-- тут ошибка -->
        <!-- <li class="list-item" v-for="email in emails" :key="emails.id">
          <div>
            <p><strong>{{email.email}}</strong></p>
            <small>{{ email.body }}</small>
          </div>
        </li> -->
      </ul>
    </div>
  </div>
</template>
<!-- случайно назвать комментарии почтами -->
<script>
export default {
  emits: ['load'],
  props: ['emails', 'wasLoaded']
}
</script>

<style scoped>

</style>
