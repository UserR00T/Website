<template>
  <div class="divider"></div>
</template>

<script>
export default {
  name: 'divider'
}
</script>

<style lang="scss">
@import "@/scss/global.scss";

.divider {
  height: 3px;
  width: 100%;
  background-color: map-get($colors, divider);
}
</style>
