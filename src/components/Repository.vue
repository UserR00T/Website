<template>
  <li @click="$emit('repoClick')">
    <img v-if="repo.owner.avatar_url" :src="repo.owner.avatar_url + '&s=32'">
    <span><a :href="repo.owner.html_url"> {{repo.owner.login}}</a>/{{repo.name}}</span>
    <span class="language" v-show="repo.language">{{repo.language}}</span>
    <a class="license" :href="'https://choosealicense.com/licenses/' + repo.license.key + '/'" v-if="repo.license">{{repo.license.name}}</a>
    <span class="fork" v-show="repo.fork">Forked // </span>
    <span class="info"><code>Stars</code><span> {{repo.stargazers_count}}</span> // <code>Forks</code><span> {{repo.forks}}</span> // <code>Watchers</code><span> {{repo.watchers_count}}</span> {{ repo.license || repo.fork ? '// ' : '' }}</span>
    <p class="description">{{repo.description}}
      <span class="date"><code>Last updated:</code> {{formatDate(new Date(repo.pushed_at))}}</span>
    </p>
  </li>
</template>

<script>
export default {
  name: 'repository',
  props: {
    repo: {
      required: true,
      type: Object
    }
  },
  methods: {
    // moment.js is a pretty big library, so that's a big nono from me.
    appendLeadingZeroes(n) {
      if(n <= 9){
        return "0" + n;
      }
      return n
    },
    formatDate(date) {
      // YYYY-MM-DD
      return date.getFullYear() + "-" 
      + this.appendLeadingZeroes(date.getMonth() + 1) + "-" 
      + this.appendLeadingZeroes(date.getDate()) + " " 

      // HH:MM:SS
      + this.appendLeadingZeroes(date.getHours()) + ":" 
      + this.appendLeadingZeroes(date.getMinutes()) + ":" 
      + this.appendLeadingZeroes(date.getSeconds())
    }
  }
}
</script>

<style lang="scss" scoped>
@import "@/scss/global.scss";

li {
  box-shadow: map-get($shadows, repository);
  background-color: map-get($colors, repository-bg);
  border-radius: 5px;
  padding: 20px;
  margin-bottom: 49px;

  &:hover {
    background-color: map-get($colors, repository-bg-hover);
    cursor: pointer;
  }

  @media (max-width: 780px) {   
    height: 80px;
  }

  @media (max-width: 550px) {   
    height: 115px;
  }
  
  @media (max-width: 500px) {   
    height: fit-content;
  }
  

  p {
    font-size: 0.6em;
    margin: 5px 0 0 10px;
    .date {
      float: right;
    }
  }
  .language {
    margin: 0 0 0 10px;
    background-color: map-get($colors, repository-el-lang);
    padding: 3px 7px;
    border-radius: 5px;
  }
  .license {
    float: right;
  }
  .fork {
    float: right;
    white-space: pre;
  }
  .info {
    float: right;
    white-space: pre;
    span {
      color: map-get($colors, repository-el-info-span);
    }
  }
  img {
    width: 32px;
    height: 32px;
    vertical-align: middle;
  }
}
</style>
