<template>
  <div class="generator">
      <h3>Generator</h3>
  </div>
</template>

<script>
import Tone from "tone";
Tone.context.latencyHint = "fastest"

export default {
  name: 'Generator',
  props: {
    params: {
      waveform: {
        type: String
      }
    }
  },
  data: function () {
    return {
      keyToPitch: { "z":"C3", "s":"C#3", "x":"D3", "d":"D#3", "c":"E3", "v":"F3", "g":"F#3", "b":"G3", "h":"G#3", "n":"A3", "j":"A#3", "m":"B3", ",":"C4", "q":"C4", "2":"C#4", "w":"D4", "3":"D#4", "e":"E4", "r":"F4", "5":"F#4", "t":"G4", "6":"G#4", "y":"A4", "7":"A#4", "u":"B4", "i":"C5", "9":"C#5", "o":"D5", "0":"D#5", "p":"E5", "[":"F5", "=":"F#5", "]":"G5", "Backspace":"G#5", "\\":"A5" }
    }
  },
  created: function () {
    window.addEventListener('keydown', this.onkeydown) 
    window.addEventListener('keyup', this.onkeyup) 
  },
  computed: {
    synth: function () {
      return new Tone.PolySynth(6, Tone.Synth, {
        oscillator : {
          type : this.params.waveform
        }
      }).toMaster();
    }
  },
  methods: {
    onkeydown(e) {
      this.synth.triggerAttackRelease(this.keyToPitch[e.key], "8n")
    }
  }
}
</script>

<style scoped>
    .generator {
        -webkit-box-shadow: 0px 6px 18px 0px rgba(0,0,0,0.35); 
        box-shadow: 0px 6px 18px 0px rgba(0,0,0,0.35);
    }

    h3 {
        margin-left: 1em;
    }
</style>
