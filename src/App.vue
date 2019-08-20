<template>
  <div id="app">
    <Page :divider="false" :fitContent="false" id="main">
      <div class="content noselect">
        <h1 class="title">Hi, I'm UserR00T</h1>
        <h2 class="main-sub">I am a backend developer.</h2>
      </div>
    </Page>

    <Page title="$ whoami">
      <MainText>{{whoami}}</MainText>
    </Page>

    <Page small title="$ cat /data.json | jq '.projects[] | &quot;\(.name)\t\(.description)&quot;'">
      <MainText>These are all the publicly released projects by me. Feel free to check them out &amp; contribute on github or their website (if existant)
        <table>
          <tr>
            <th>Name</th>
            <th>Description</th>
            <th></th>
          </tr>
          <Project v-for="(project, index) in projects" :key="index"
            :name="project.name"
            :description="project.description"
            :website="project.website"
            :github="project.github"
          />
        </table>
      </MainText>
    </Page>

    <Page xs title="$ curl https://api.github.com/users/UserR00T/repos?sort=updated&amp;type=all">
      <MainText>These are all my <i>public</i> repositories, fetched from the github API. May contain duplicates from the projects page. Sorted by last updated, descending order.
        <ul class="repositories">
          <Repository v-for="(repo, index) in repositories" :key="index" :repo="repo" @click="goto(repo.html_url)"/>
        </ul>
      </MainText>
    </Page>

    <Page small title="$ nano skills.txt">
      <div v-for="(skill, index) in skills" :key="index"> 
        <Title sub >{{skill.name}}</Title>
        <MainText>{{skill.text}}</MainText>
      </div>
    </Page>


    <Page small title="$ vi contact.txt">
      <MainText>
        <ul class="contact">
          <li v-for="(contact, index) in contacts" :key="index"><a :href="contact.href">{{contact.name}}</a> // </li>
          <li>:wq</li>
        </ul>
      </MainText>
    </Page>
    
    <Page :fitContent="true" class="footer">
      <div>
        <p>Hand crafted with <span style="color: #ff000057;">&lt;3</span> by UserR00T. (c) 2019</p>
      </div>
    </Page>
  </div>
</template>

<script>
import Page from './components/Page';
import MainText from './components/MainText';
import Title from './components/Title';
import Project from './components/Project';
import Repository from './components/Repository';

export default {
  name: 'app',
  components: {
    Page,
    MainText,
    Title,
    Project,
    Repository
  },
  methods: {
    fetch(url, options) {
      return fetch(url, options).then(response => response.json());
    },
    goto(url) {
      window.location.href = url;
    }
  },
  mounted() {
    VANTA.TOPOLOGY({
      el: "#main",
      color: 0xe31421,
      backgroundColor: 0x201208
    })
    this.fetch('data.json').then((content) => {
      this.whoami = content.whoami;
      this.projects = content.projects;
      this.skills = content.skills;
      this.contacts = content.contacts;
      this.repoUrl = content.repoUrl;
      this.fetch(this.repoUrl, {
        method: 'GET',
        headers: {
          Accept: 'application/vnd.github.mercy-preview+json'
        }
      }).then((repositories) => {
         this.repositories = repositories;
      });
    });
  },
  data() {
    return {
      projects: [],
      skills: [],
      whoami: undefined,
      contacts: [],
      repositories: [],
      repoUrl: undefined
    }
  }
}
</script>

<style lang="scss">
@import "@/scss/global.scss";

ul {
  padding-left: 0;
  list-style-type: none;
  &.contact li {
    display: inline;
  }
}

::-webkit-scrollbar {
  width: map-get($scrollbar, width);
  height: map-get($scrollbar, height);
}
::-webkit-scrollbar-thumb {
  background: map-get($scrollbar, thumb);
}
::-webkit-scrollbar-track {
  background: map-get($scrollbar, track);
}

* {
  color: map-get($colors, text-default);
}
a[href] {
  text-decoration: none;
  color: map-get($colors, href);
}
p {
  white-space: pre-line;
}


table {
  margin: 0 5% 0 0;
  width: 100%;
  th {
    text-align: left;
    background-color: map-get($colors, table-header);
  }
  td, th {
    padding: 8px;
  }
  td {
    border-bottom: 1px solid map-get($colors, table-border);
    @media (max-width: 780px) {   
      font-size: 0.8em;
    }
  }
  > tr:last-child > td {
    border-bottom: 0;
  }
  td:nth-child(1) {
    max-width: 2vw;
  }
  td:nth-child(2) {
    max-width: 15vw;
  }
  td:nth-child(3) {
    max-width: 2vw;
  }
  tr:hover {
    background-color: darken(map-get($colors, background), 1%);
  }
}

.footer {
  .fit-content {
    padding-bottom: 0;
  }
  p {
    text-align: center;
    color: map-get($colors, footer-text);
  }
}

.main-sub {
  font-family: map-get($fonts, main-sub);
  font-size: 2em;
  font-weight: 100;
}

.content {
  text-align: center;
  margin: 0 25%;
  padding: 0 0 3vh 0;
}

.noselect {
  -webkit-touch-callout: none;
    -webkit-user-select: none;
     -khtml-user-select: none;
       -moz-user-select: none;
        -ms-user-select: none;
            user-select: none;
}

body {
  overflow-x: hidden;
  background-color: map-get($colors, background);
}

html, body {
  margin: 0;
  padding: 0;
}
#main {
  padding: 20vh 0 0;
}

#app {
  font-family: map-get($fonts, main);
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
