<template>
  <div class="header">
    <h1 class="header__title">
      Text Editor
    </h1>
  </div>
</template>
<script>
export default {
  name: 'Header'
}
</script>
<style scoped>
.header {
  padding: 1rem;
  background: var(--primary);
  color: #fff;
  grid-column: 1/13;
  grid-row: 1;
}
.header__title {
  font-weight: 700;
  font-size: 1.75rem;
  text-align: center;
}
</style>