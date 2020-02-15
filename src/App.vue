<template>
  <div id="app">
    <Header />
    <InputSection v-on:add-shapes="addShapes"/>
    <SVGOutput v-bind:commands="commands" />
  </div>
</template>

<script>
import Header from './components/layout/Header'
import InputSection from './components/InputSection'
import SVGOutput from './components/SVGOutput'

export default {
  name: 'App',
  components: {
    Header,
    InputSection,
    SVGOutput
  },
  data() {
    return {
      commands: []
    }
  },
  methods: {
    addShapes(commands) {
      console.log(commands);
      this.commands = commands;
    }
  }
}
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
      -webkit-font-smoothing: antialiased;
      -moz-osx-font-smoothing: grayscale;
    text-align: center;
    background: #e0e0e0;
  }
</style>
