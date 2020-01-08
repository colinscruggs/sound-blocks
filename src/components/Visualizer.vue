<template>
  <div class="visualizer">
      <h3>Visualizer</h3>
      <canvas id="pts"></canvas>
  </div>
</template>

<script>
import Tone from "tone";
import { CanvasSpace, Sound, Pt } from "pts";
//import {CanvasSpace, Sound, Pt, Group, Line } from "pts";
Tone.context.latencyHint = "fastest";

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
    window.addEventListener('keydown', this.onkeydown);
    window.addEventListener('keyup', this.onkeyup);
  },
  mounted: function() {
    var space = new CanvasSpace("#pts")
    space.setup({ bgcolor: "white", retina: true});

    var form = space.getForm();

    let sound = Sound.from( this.synth, this.synth.context ).analyze(256);
    // TODO: add this shit to a function that is called every time something changes
    space.add( {
        animate: () => { 
          let area = space.size;
          let rect = [new Pt([0,0]), area];
          
          let freqs = sound.freqDomainTo( [area.x, area.y], [rect[0].x, rect[0].y] ).map(
            f => [
              [f.x, rect[0].y + area.y/2-f.y],
              [f.x, rect[0].y + area.y/2+f.y]
            ] );
          form.strokeOnly("black", Math.ceil(area.x) ).lines( freqs );
        },

      action: (type) => {
          if (type === "up") { // for safari
            if (this.synth.context.state === 'suspended') {
              this.synth.context.resume();
            }
          }
        }
    });

    space.bindMouse().bindTouch().play();
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
    .visualizer {
        -webkit-box-shadow: 0px 6px 18px 0px rgba(0,0,0,0.35); 
        box-shadow: 0px 6px 18px 0px rgba(0,0,0,0.35);
    }

    h3 {
        margin-left: 1em;
    }

    #pts {
      min-width: 100%;
      min-height: 100%;
    }
</style>
