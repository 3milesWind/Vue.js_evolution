<template>
  <!-- <h2 v-for="name in names" v-bind:key="name">{{ name }}</h2> -->
  <h2 v-for="(name,index) in names" v-bind:key="name">{{ index }} {{ name }}</h2>
  <h2 v-for="name in fullName" :key="name.first">{{ name.first }} {{name.last}}</h2>
  
  <div v-for="actor in actors" :key="actor.name">
    <h2>{{ actor.name}}</h2>
    <h3 v-for="movie in actor.movies" :key="movie">{{movie}}</h3>
  </div>

  <h2 v-for="(value, key, index) in myInfor" :key="value">{{index}} {{key}} {{ value}}</h2>
  
  <template v-for="name in names" :key="name">
    <h2 v-if="name === 'Bruce'"> {{name}}</h2>
  </template>

<template v-for="name in names" :key="name"> 
  <h2>{{name}}</h2>
  <hr />
</template>

</template>
<script>
export default {
  name: 'App',
  data() {
    return {
      names: ['Bruce', 'Clark', 'Diana'],
      fullName:[
        {first: 'Bruce', last: 'Wayne'},
        {first: 'Bruce2', last: 'Wayne2'},
        {first: 'Bruce3', last: 'Wayne3'},
      ],
      actors:[
        {
          name: "jeffrey",
          movies: ['Batman', 'The Prestige'],
        },
        {
          name:"Di caprio",
          movies: ['Titanic', 'Inception']
        }
      ],
      myInfor:{
          name: 'Vishwas',
          channel: 'CodeVolution'
      }
    };
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
