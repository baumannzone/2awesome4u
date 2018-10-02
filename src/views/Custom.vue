<template>
  <div class="about">
    <h1>Custom params</h1>
    <form>
      <label for="voiceList">Voice: </label>
      <select id="voiceList" v-model="selectedVoiceName">
        <option value="0">Choose voice...</option>
        <option v-for="(v, idx) in voiceNames" :value="v.name" :key="idx">{{ v.name }} {{ v.lang }}</option>
      </select>

      <label for="text">Text: </label>
      <input id="text" type="text" v-model="text">

      <label for="rate">Rate (Speed): </label>
      <input type="range" id="rate" v-model="rate" min="0.46" max="3.6" step="0.01">
      <p>{{ rate }}</p>

      <label for="pitch">Pitch (Tone): </label>
      <input type="range" id="pitch" v-model="pitch" min="0" max="2" step="0.05">
      <p>{{ pitch }}</p>

    </form>
    <br>
    <button @click="playText">Play ▶︎</button>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      rate: 1,
      pitch: 1,
      voiceNames: [],
      voices: [],
      selectedVoiceName: 0,
      text: 'Mi perro se llama rambo 🐶'
    }
  },
  created () {
    // Check support for speech API
    if (typeof speechSynthesis !== 'undefined' && speechSynthesis.onvoiceschanged !== undefined) {
      speechSynthesis.onvoiceschanged = this.populateVoiceList
    } else {
      console.warn('Nope!')
    }
  },
  methods: {
    // List of voices
    populateVoiceList () {
      this.voices = window.speechSynthesis.getVoices()
      this.voiceNames = this.voices.map((v) => {
        return { name: v.name, lang: v.lang }
      })
    },
    playText () {
      const synth = window.speechSynthesis
      // Find selected voice
      const voice = this.voices.find(v => v.name === this.selectedVoiceName)
      // Next we create a new speech synthesis utterance (pronunciación)
      const utterThis = new SpeechSynthesisUtterance(this.text)
      utterThis.voice = voice
      utterThis.pitch = this.pitch
      utterThis.rate = this.rate
      console.log('utterThis:')
      console.log(utterThis)
      synth.speak(utterThis)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" scoped>
  label
    display block
    font-size 18px
    font-weight bold
    font-family monospace
    margin-top 40px

  input[type="text"]
    width 300px
    padding 2px 5px
    font-size 18px

  select
    font-size 18px

  input[type="range"]
    width 300px
  p
    font-family monospace
    color #42b983
    margin-top 0
    font-size 20px
</style>
