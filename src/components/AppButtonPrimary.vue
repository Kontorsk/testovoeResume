<template>
  <div>
    <p>
      <button class="primary">Загрузить комментарии</button>
    </p>
  </div>
</template>

<script>
export default {
  emits: ["load"],
};
</script>

<style scoped>
.primary {
  position: relative;
  place-content: center;
  place-items: center;
  width: fit-content;
  border-radius: 99px;
  letter-spacing: 0.05em;
  border: 1px solid #42b983;
  text-decoration: none;
  text-transform: uppercase;
  margin-right: 10px;
  padding: 0.5rem 1.5rem;
  white-space: nowrap;
  font-weight: 700;
  outline: none;
  transition: all 0.22s;
  background: #42b983;
  color: #fff;
  cursor:pointer
}
</style>
