<template>
  <tr v-show="name">
    <td>{{name}}</td>
    <td>{{description}}</td>
    <td v-if="extraContent" class="text-url">{{extraContent}}</td>
    <td v-else>
      <a :href="website" v-show="website">Website</a>
      <span v-show="website && github"> // </span>
      <a :href="github" v-show="github">Github</a>
    </td>
  </tr>
</template>

<script>
export default {
  name: 'project',
  props: {
      name: {
        default: undefined,
        type: String
      },
      description: {
        default: undefined,
        type: String
      },
      website: {
        default: undefined,
        type: String
      },
      github: {
        default: undefined,
        type: String
      },
      extraContent: {
        default: undefined,
        type: String
      }
  }
}
</script>