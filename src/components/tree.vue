<!-- Demo1Easiest.vue -->
<template>
  <Tree :value="treeData">
    <span slot-scope="{node, index, path, tree}">
      <input type="checkbox" :checked="node.$checked" @change="tree.toggleCheck(node, path)" />
      {{node.text}}<button>Add</button>
    </span>
  </Tree>
</template>
<script>
import 'he-tree-vue/dist/he-tree-vue.css'
import {Tree, Draggable} from 'he-tree-vue'

export default {
  components: {Tree: Tree.mixPlugins([Draggable])},
  data() {
    return {
      treeData: [
          {text: 'node 1'}, 
          {text: 'node 2', 
            children: [
                {text: 'node 2-1', 
                    children: [
                        {text: 'node 2-1-1'}
                    ]
                }
            ]
          }
       ]
    }
  }
  
}
</script>