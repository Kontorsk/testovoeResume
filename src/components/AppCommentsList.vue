<template>
  <div>
    <p>
      <button class="btn primary" @click="$emit('load')">Загрузить комментарии</button>
    </p>
    <div class="card" v-if="wasLoaded">
      <h2>Комментарии</h2>
      <ul class="list">
        <li class="list-item" v-for="email in emails" :key="emails.id">
          <div>
            <p><strong>{{email.email}}</strong></p>
            <small>{{ email.body }}</small>
          </div>
        </li>
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