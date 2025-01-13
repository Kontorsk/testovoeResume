<template>
    <h1 @click.right.prevent="$emit('remove')">{{ $attrs.value }}</h1>
</template>

<script>
export default {
  emits: ["remove"],
};
</script>
