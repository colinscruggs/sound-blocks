<template>
  <div id="app">
    <Title id="title"/>
    <Generator id="generator"/>
    <Resources id="resources"/>
    <Vis id="vis"/>
  </div>
</template>

<script>
import Title from './components/Title.vue'
import Generator from './components/Generator.vue'
import Resources from './components/Resources.vue'
import Vis from './components/Vis.vue'

export default {
  name: 'app',
  components: {
    Title,
    Generator,
    Resources,
    Vis
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;

  display: grid;
  grid-template-areas: 
    "title title title"
    "generator vis vis"
    "generator resources resources";
  grid-template-rows: 5rem 60% auto;
  grid-gap: 1rem;

  min-height: 95vh;
  min-width: 90vw;
}

#title {
  grid-area: title;
}

#generator {
  grid-area: generator;
}

#resources {
  grid-area: resources;
}

#vis {
  grid-area: vis;
}
</style>
