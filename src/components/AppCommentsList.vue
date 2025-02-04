<template>
  <app-button @click="$emit('load')" class="btn primary">
    Загрузить комментарии
  </app-button>
  <div v-if="comments.length" class="card">
    <h2>Комментарии</h2>
    <ul class="list">
      <li v-for="comment in comments" :key="comment.id" class="list-item">
        <div>
          <p>
            <strong>{{ comment.email }}</strong>
          </p>
          <small>{{ comment.body }}</small>
        </div>
      </li>
    </ul>
  </div>
  <app-loader v-if="loadingComments" />
</template>
<script>
import AppButton from './AppButton.vue';
import AppLoader from './AppLoader.vue';

export default {
  components: {
    AppButton,
    AppLoader,
  },
  props: ['comments', 'loadingComments'],
  emits: ['load'],
};
</script>

<style scoped></style>
