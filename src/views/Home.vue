<template>
  <div class="home">
    <h1>Speech API</h1>
    <label for="text">Text: </label>
    <input type="text" v-model="text" id="text">
    <p> {{ text }} </p>
    <button @click="play">Play ▶</button>
  </div>
</template>

<script>
export default {
  name: 'Home',
  data () {
    return {
      text: 'Hola, soy Jorge Baumann, y te presento la API de pronunciación del navegador'
    }
  },
  created () {
    // Check support for speech API
    if (typeof speechSynthesis !== 'undefined' && speechSynthesis.onvoiceschanged !== undefined) {
      this.play()
    } else {
      console.warn('Nope!')
    }
  },
  methods: {
    play () {
      const synth = window.speechSynthesis
      const utterThis = new SpeechSynthesisUtterance(this.text)
      synth.speak(utterThis)
    }
  }
}
</script>

<style lang="stylus" scoped>
  p
    padding-left 10%
    padding-right 10%
    font-size 20px

  input
    width 400px
    margin-left 10px
    padding 2px 5px
    font-size 15px

  button
    font-size 20px
</style>
