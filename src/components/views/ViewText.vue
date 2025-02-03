<template>
  <div>
    <p @click.right.prevent="$emit('remove')">
      {{ $attrs.value }}
    </p>
  </div>
</template>

<script>
export default {
  emits: ['remove'],
};
</script>
