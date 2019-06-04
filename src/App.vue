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

    <Page small title="$ cat /projects.json  | jq -r '.[] | &quot;\(.name)\t\(.description)&quot;'">
      <MainText>These are all the publicly released projects by me. Feel free to check them out & contribute on github or their website (if existant)

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


    <Page small title="console.log(JSON.Parse(data).skills);">
      <div v-for="(skill, index) in skills" :key="index"> 
        <Title sub >{{skill.name}}</Title>
        <MainText>{{skill.text}}</MainText>
      </div>
    </Page>


    <Page small title="$ vi contact.txt">
      <MainText>
        <ul>
          <li>// </li>
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

export default {
  name: 'app',
  components: {
    Page,
    MainText,
    Title,
    Project
  },
  methods: {
    readFile(file, callback) {
      var rawFile = new XMLHttpRequest();
      rawFile.overrideMimeType("application/json");
      rawFile.open("GET", file, true);
      rawFile.onreadystatechange = function() {
          if (rawFile.readyState === 4 && rawFile.status === 200) {
              callback(rawFile.responseText);
          }
      }
      rawFile.send(null);
    }
  },
  mounted() {
    VANTA.TOPOLOGY({
      el: "#main",
      color: 0xe31421,
      backgroundColor: 0x201208
    })
    this.readFile('data.json', (content) => {
      var obj = JSON.parse(content);
      this.whoami = obj.whoami;
      this.projects = obj.projects;
      this.skills = obj.skills;
      this.contacts = obj.contacts;
    });
  },
  data() {
    return {
      projects: [],
      skills: [],
      whoami: undefined,
      contacts: []
    }
  }
}
</script>

<style lang="scss">
ul {
  padding-left: 0;
  li {
    display: inline;
  }
}
::-webkit-scrollbar {
  width: 0.5em;
  height: 0.5em;
}
::-webkit-scrollbar-thumb {
  background: #737373;
}
::-webkit-scrollbar-track {
  background: #b8c0c838;
}
body {
  overflow-x: hidden;
}

* {
  color: white;
}
a[href] {
  text-decoration: none;
  color: #969696;
}
p {
  white-space: pre-line;
}


table {
  margin: 0 5% 0 0;
  width: 100%;
  th {
    text-align: left;
    background-color: rgba(59, 54, 50, 0.7);
  }
  td, th {
    padding: 8px;
  }
  td {
    border-bottom: 1px solid rgba(59, 54, 50, 0.4);
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
    background-color: #271717;
  }
}
.footer {
  .fit-content {
    padding-bottom: 0;
  }
  p {
    text-align: center;
    color: #807f7f;
  }
}
.main-sub {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
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

html, body {
  margin: 0;
  padding: 0;
}
#main {
  padding: 20vh 0 0;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
