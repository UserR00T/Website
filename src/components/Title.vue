<template>
  <h2 class="title" :class="{ 'sub': sub, 'small': small, 'xs': xs }">
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
      xs: {
        default: false,
        type: Boolean
      },
  }
}
</script>

<style lang="scss">
@import "@/scss/global.scss";

.title {
  margin-left: 10px;
  font-family: map-get($fonts, title);
  font-size: 5em;
  font-weight: 100;
  &.small {
    font-size: 3.5em;
  }
  &.sub {
    font-size: 2.5em;
  }
  &.xs {
    font-size: 2.5em;
  }
  @media (max-width: 700px) { 
    font-size: 4em;
    &.small {
      font-size: 2.5em;
    }
    &.sub {
      font-size: 1.5em;
    }
    &.xs {
      font-size: 1.5em;
    }
  }

  @media (max-width: 500px) { 
    font-size: 3em;
    &.small {
      font-size: 1.5em;
    }
    &.sub {
      font-size: 1.5em;
    }
    &.xs {
      font-size: 1em;
    }
  }
}
</style>
