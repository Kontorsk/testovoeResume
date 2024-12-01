<template>
  <div>
    <h1 @click.right.prevent="$emit('remove')">{{$attrs.value}}</h1>
  </div>
</template>

<script>
export default {
  emits: ['remove']
}
</script>
