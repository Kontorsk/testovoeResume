<template>
  <div class="avatar">
    <img :src="$attrs.value" @click.right.prevent="$emit('remove')" />
  </div>
</template>

<script>
export default {
  emits: ["remove"],
};
</script>
