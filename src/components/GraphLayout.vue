<template>
  <div class='graph-layout-container'>
  </div>
</template>

<script>
import bus from '../lib/bus.js'
import Viva from 'vivagraphjs'

export default {
  data () {
    return {
    }
  },
  ready () {
    bus.on('render-graph', updateRenderer, this)
  },

  destroyed () {
    bus.off('render-graph', updateRenderer)
  }

}

function updateRenderer(graph) {
  console.log(graph, this)
  if (this.renderer) {
    this.renderer.dispose()
  }

  var graphics = Viva.Graph.View.webglGraphics()
  var renderer = Viva.Graph.View.renderer(graph, {
    graphics,
    container: this.$el
  })
  renderer.run()
  this.renderer = renderer
}
</script>

<style lang="stylus">
.graph-layout-container {
  position: relative;

  svg {
    width: 100%;
    height: 100%;
    position: absolute;
  }
}
</style>
