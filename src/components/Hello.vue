<template>
  <div class="hello">
    <div v-if="github" class="hello__content">
      <div class="hello__avatar" v-bind:style="{ backgroundImage: 'url(' + github.avatar_url + ')' }">
      </div>
      <h1>{{ name }}</h1>
      <h2>Front-end Engineer</h2>
      <span>{{ github.location }}</span>
      <span>GitHub repos: <a v-bind:href="github.html_url">{{ github.public_repos }}</a></span>
      <span>Say <a href="mailto:mail@stevengeorgeharris.com">hello!</a></span>
    </div>
  </div>
</template>

<script>

import Axios from 'axios'

const GIT_URL = 'https://api.github.com/users/stevengeorgeharris'

export default {
  name: 'hello',
  data () {
    return {
      name: 'Steven Harris',
      github: null
    }
  },
  created () {
    Axios.get(GIT_URL)
      .then(res => {
        this.github = res.data
      })
      .catch(e => {
        console.log(e)
      })
  }
}
</script>

<style scoped>
h1 {
  font-weight: 700;
  margin-bottom: 0;
}

h2 {
  font-weight: 500;
  margin: .2em 0 .6em 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #fff;
  font-weight: bold;
  text-decoration: none;
  border-bottom: 1px solid #fff;
  transition: all ease-in-out 200ms;
}

a:hover {
  padding-bottom: .2em;
}

.hello__content {
  margin-bottom: 2em;
}

.hello__avatar {
  width: 100px;
  height: 100px;
  overflow: hidden;
  margin: 0 auto;
  border: 3px solid #fff;
  border-radius: 50%;
  position: relative;
  background-size: cover;
  background-position: center;

  transition: all ease-in-out 100ms;
}

.hello__avatar:hover {
  border-width: 5px;
}

.hello {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
}

span {
  font-size: 1.5em;
  display: block;
}
</style>
