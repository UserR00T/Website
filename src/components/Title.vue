<template>
  <h2 class="title" :class="{ 'sub': sub, 'small': small }">
    <slot>
      No content specified.
    </slot>
  </h2>
</template>

<script>
export default {
  name: 'text-title',
    props: {
      sub: {
        default: false,
        type: Boolean
      },
      small: {
        default: false,
        type: Boolean
      },
  }
}
</script>

<style lang="scss">
.title {
  margin-left: 10px;
  font-family: 'Lato', sans-serif;
  font-size: 5em;
  font-weight: 100;
  &.small {
    font-size: 3.5em;
  }
  &.sub {
    font-size: 2.5em;
  }
}
</style>
