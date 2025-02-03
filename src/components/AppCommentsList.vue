<template>
  <div>
    <app-button-primary @click="$emit('load')" />
    <div class="card" v-if="comments.length">
      <h2>Комментарии</h2>
      <ul class="list">
        <li class="list-item" v-for="comment in comments" :key="comment.id">
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
  </div>
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
