<template>
  <div id="app">
    <Start v-if="!started" @start="started = true"/>
    <Question @back="started = false" v-else/>
  </div>
</template>

<script>
import Start from './components/Start.vue'
import Question from './components/Question.vue'
export default {
  name: 'App',
  components: {
    Start,
    Question
  },
  data(){
    return {
      started: false
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto&display=swap');

* {
  font-family: 'Roboto', sans-serif;
  color: #fff;
}

body, html {
  margin: 0;
  padding: 0;
  background: #121214;
}

button {
  border: none;
  outline: none;
  padding: 15px 25px;
  background: #835ae4;
  font-size: 1.3rem;
  border-radius: 9px;
  cursor: pointer;
}
</style>
