<template>
  <div id="app">
    <VueCytoscape :config="config">
      <CyElement
        v-for="def in elements"
        :key="`${def.data.id}`"
        :definition="def"
        v-on:mousedown="elementClicked($event, def.data.id)"
      />
    </VueCytoscape>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import { VueCytoscape, CyElement } from 'vue-cytoscape'

@Component({
  components: {
    VueCytoscape,
    CyElement
  }
})
export default class App extends Vue {
  elementClicked($event: any, id: string) {
    console.log(`element ${id} clicked`)
  }

  config = {
    style: [
      {
        selector: 'node',
        style: {
          'background-color': '#666',
          label: 'data(id)'
        }
      },
      {
        selector: 'edge',
        style: {
          width: 3,
          'line-color': '#ccc',
          'target-arrow-color': '#ccc',
          'target-arrow-shape': 'triangle'
        }
      }
    ],
    layout: {
      name: 'grid',
      rows: 1
    }
  }

  elements = [
    {
      // node a
      data: { id: 'a' },
      position: { x: 100, y: 100 },
      group: 'nodes'
    },
    {
      // node b
      data: { id: 'b' },
      position: { x: 400, y: 100 },
      group: 'nodes'
    },
    {
      // edge ab
      data: { id: 'ab', source: 'a', target: 'b' },
      group: 'edges'
    }
  ]
}
</script>
