<template>
  <div>
    <h2 @click.right.prevent="$emit('remove')">{{$attrs.value}}</h2>
  </div>
</template>

<script>
export default {
  emits: ['remove']
}
</script>
