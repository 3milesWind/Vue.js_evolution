<template>
  <!-- <Greet name = 'Burce'/>
  <Greet name = 'Clark'/>
  <Greet :name = 'name'/> -->
  <Article id="my-id-attribute" title='good' :like='50' :isPublished="true"/>
</template>

<script>
// import Greet from './components/Greet.vue'
import Article from './components/Article.vue'
export default {
  name: 'App',
  components: {
    // Greet,
    Article,
  },
  data() {
    return {
      name: 'batman'
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
