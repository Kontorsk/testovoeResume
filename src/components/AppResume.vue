<template>
  <div
    v-if="blocks.length"
    class="card card-w70"
  >
    <component
      v-for="block in blocks"
      :key="block.id"
      :is="'view-' + block.type"
      :value="block.value"
      @remove="$emit('removeBlock', block.id)"
    >
    </component>
  </div>
  <app-loader v-else-if="loadingBlocks" />
  <div
    v-else
    class="card card-w70"
  >
    <h3>Добавьте первый блок, чтобы увидеть результат</h3>
  </div>
</template>

<script>
import AppLoader from './AppLoader.vue';
import ViewAvatar from './views/ViewAvatar.vue';
import ViewSubtitle from './views/ViewSubtitle.vue';
import ViewText from './views/ViewText.vue';
import ViewTitle from './views/ViewTitle.vue';

export default {
  components: {
    ViewAvatar,
    ViewText,
    ViewSubtitle,
    ViewTitle,
    AppLoader,
  },
  props: {
    blocks: {
      type: Array,
      required: true,
    },
    loadingBlocks: {
      type: Boolean,
      required: true,
    },
  },
};
</script>

<style scoped>
.card-loading {
  padding: 1rem;
  margin-bottom: 1rem;
  border-radius: 10px;
  background: #fff;
  width: 70%;
}
</style>
