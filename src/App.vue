<template>
  <div id="app">
    <graph-text-input></graph-text-input>
    <graph-layout></graph-layout>
  </div>
</template>

<script>
import GraphTextInput from './components/GraphTextInput'
import GraphLayout from './components/GraphLayout'

export default {
  components: {
    GraphTextInput,
    GraphLayout
  }
}
</script>

<style>
html {
  height: 100%;
}

body {
  position: absolute;
  overflow: hidden;
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
}

#app {
  color: #2c3e50;
  font-family: Source Sans Pro, Helvetica, sans-serif;
  display: flex;
  flex-direction: row;
  height: 100%;
}

.graph-text-input-container {
  width: 300px;
  height: 100%;
}

.graph-layout-container {
  flex: 1;
}
</style>
