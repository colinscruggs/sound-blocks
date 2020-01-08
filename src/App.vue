<template>
  <div id="app">
    <Title id="title"/>

    <Visualizer id="visualizer"
      :params=selectedParams
    />

    <div id="control-panel">
      <h3>Control Panel</h3>
        <div id="container">
          <div id="waveforms" class="bin">
            <h4>Waveform</h4>
            <Block v-for="(value, name) of waveforms" 
              v-on:click.native="() => selectedParams.waveform = name"
              :key="name"
              :value="name"
              :type="'waveform'"
              :selected="name === selectedParams.waveform ? true : false"
            />
          </div>
        </div>
    </div>

  </div>
</template>

<script>
import Title from './components/Title.vue'
import Visualizer from './components/Visualizer.vue'
import Block from './components/Block.vue'

export default {
  name: 'app',
  components: {
    Title,
    Visualizer,
    Block
  },
  data: function () {
    return {
      waveforms: { 
        sine: 'sine',
        square: 'square',
        triangle: 'triangle',
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
        waveform: 'sine'
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

  #visualizer {
    flex: 1 1;
    margin: 1em;
  }

  #control-panel {
    flex: 0 1;
    margin: 1em;
    -webkit-box-shadow: 0px 6px 18px 0px rgba(0,0,0,0.35); 
    box-shadow: 0px 6px 18px 0px rgba(0,0,0,0.35);
    background-color: #333333;
    color: #fafafa;
  }

  #control-panel h3 {
    margin-left: 1em;
  }

  #container {
    margin: 0em 2em 1em 2em;
    display: flex;
    width: 100%;
  }

  .bin {
    background-color: #cccccc;
    max-width:fit-content;
    padding: 0.5em;
  }

  .bin h4 {
    margin: 0;
  }
</style>
