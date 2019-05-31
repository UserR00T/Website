<template>
  <p class="text">
    <slot></slot>
  </p>
</template>

<script>
export default {
  name: 'main-text'
}
</script>

<style>
.text {
  margin: 0 5%;
  font-size: 1.4em;
}
</style>
