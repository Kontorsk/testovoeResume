<template>
  <h2 @click.right.prevent="$emit('remove')">{{ $attrs.value }}</h2>
</template>

<script>
export default {
  emits: ['remove'],
};
</script>
