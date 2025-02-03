<template>
  <p @click.right.prevent="$emit('remove')">
    {{ $attrs.value }}
  </p>
</template>

<script>
export default {
  emits: ['remove'],
};
</script>
