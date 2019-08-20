<template>
  <div>
    <Divider v-show="divider"/>
    <div :class="{ 'full': !fitContent, 'fit-content': fitContent }">
      <Title :sub="sub" :small="small" :xs="xs" v-show="title">{{title}}</Title>
      <slot></slot>
    </div>
  </div>
</template>

<script>
import Title from './Title';
import Divider from './Divider';
export default {
  name: 'page',
  components: {
    Title,
    Divider
  },
  props: {
      title: {
        default: undefined,
        type: String
      },
      small: {
        default: false,
        type: Boolean
      },
      sub: {
        default: false,
        type: Boolean
      },
      xs: {
        default: false,
        type: Boolean
      },
      fitContent: {
        default: true,
        type: Boolean
      },
      divider: {
        default: true,
        type: Boolean
      }
  }
}
</script>

<style>
.fit-content {
  padding-bottom: 30px;
}
.full {
  height: 100vh;
}
</style>
