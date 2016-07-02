<template>
  <div class='graph-text-input-container'>
    <div class='error' v-show='error'>{{error}}</div>
    <div v-el:editor class='graph-text-input'></div>
    <div class='fotter'>
      <button @click='sendGraphForLayout'>Layout</button>
    </div>
  </div>
</template>

<script>
import CodeMirror from 'codemirror'
import miserables from 'miserables'
import todot from 'ngraph.todot'
import fromDot from 'ngraph.fromdot'
import bus from '../lib/bus.js'

export default {
  data () {
    let content = '// Enter your .dot file below\n// and click "Layout"\n// E.g.:\n'
    content += todot(miserables)

    return {
      content,
      error: ''
    }
  },

  methods: {
    sendGraphForLayout () {
      let content = this.editor.getValue()
      try {
        let graph = fromDot(content)
        this.error = ''
        bus.fire('render-graph', graph)
      } catch (e) {
        this.error = e.message + ' @line ' + e.location.start.line
        console.log(e)
      }
    }
  },

  ready () {
    this.editor = CodeMirror(this.$els.editor, {
      lineNumbers: true,
      value: this.content
    })
  }
}
</script>

<style lang="stylus">
@import '../../node_modules/codemirror/lib/codemirror.css';

.graph-text-input-container {
  display: flex;
  flex-direction: column;
  border-right: 1px solid #efefef;
  .graph-text-input {
    flex: 1;
    overflow: hidden;
  }

  .CodeMirror {
    height: 100%;
  }

  .error {
    color: red;
    border-bottom: 1px solid red;
    padding: 7px;
  }
}


</style>
