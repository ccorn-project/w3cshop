<script setup>
import { h, ref } from 'vue'
import { Background } from '@vue-flow/background'
import { Controls } from '@vue-flow/controls'
import { MiniMap } from '@vue-flow/minimap'
import { VueFlow, useVueFlow } from '@vue-flow/core'
import CustomNode from './CustomNode.vue'
import CustomEdge from './CustomEdge.vue'

const { onConnect, addEdges } = useVueFlow()

const nodes = ref([
  { id: '1', type: 'input', label: 'Node 1', position: { x: 250, y: 5 } },
  { id: '2', type: 'output', label: 'Node 2', position: { x: 100, y: 100 } },
  { id: '3', type: 'custom', label: 'Node 3', position: { x: 400, y: 100 } },
])

const edges = ref([
  { id: 'e1-2', source: '1', target: '2', type: 'custom' },
  { id: 'e1-3', source: '1', target: '3', animated: true },
])

onConnect((params) => {
  addEdges([params])
})
</script>

<template>
  <div style="height: 100vh">
    <VueFlow
      v-model:nodes="nodes"
      v-model:edges="edges"
      fit-view-on-init
      class="vue-flow-basic-example"
      :default-zoom="1.5"
      :min-zoom="0.2"
      :max-zoom="4"
    >
      <Background pattern-color="#aaa" :gap="8" />

      <MiniMap />

      <Controls />

      <template #node-custom="nodeProps">
        <CustomNode v-bind="nodeProps" />
      </template>

      <template #edge-custom="edgeProps">
        <CustomEdge v-bind="edgeProps" />
      </template>
    </VueFlow>
  </div>
</template>
