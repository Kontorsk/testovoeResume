<template>
  <app-button-primary @click="$emit('load')" />
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
import AppButtonPrimary from './AppButtonPrimary.vue';
import AppLoader from './AppLoader.vue';

export default {
  components: {
    AppButtonPrimary,
    AppLoader,
  },
  props: ['comments', 'loadingComments'],
  emits: ['load'],
};
</script>

<style scoped></style>
