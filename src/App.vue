<template>
  <div id="app">
    <Title id="title"/>
    <Generator 
      id="generator"
      :waveform=selectedParams.waveform />
    <Resources id="resources"/>
  </div>
</template>

<script>
import Title from './components/Title.vue'
import Generator from './components/Generator.vue'
import Resources from './components/Resources.vue'

export default {
  name: 'app',
  components: {
    Title,
    Generator,
    Resources
  },
  data: function () {
    return {
      waveform: { 
        sine: 'sine',
        square: 'square',
        triange: 'triangle',
        sawtooth: 'sawtooth'
      },
      volumeEnv: {
        attack: 0.01,
        decay: 0.1,
        sustain: 0.5,
        release: 1
      },
      volumeEnvCurves: {
        attackCurve: 'linear',
        decayCurve: 'exponential',
        releaseCurve: 'exponential'
      },
      selectedParams: {
        waveform: 'square'
      }
    }
  }
}
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;

    display: flex;
    flex-direction: column;

    min-height: 95vh;
    min-width: 90vw;
  }

  #title {
    height: 5em;
    flex: 0;
  }

  #generator {
    flex: 1 1;
    margin: 1em;
  }

  #resources {
    flex: 1.5 1;
    margin: 1em;
  }
</style>
