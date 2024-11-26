<script setup lang="ts">
import {IntTreeFolderList} from "../model/treeFolderList.ts";

import NodeTree from "./ui/NodeTree.vue";

defineProps<{
  treeNodes: IntTreeFolderList[]
}>()

const currentSelectedId = defineModel<null | number>('selectedId')

</script>

<template>
  <ul class="tree-folder-list__wrapper">
    <node-tree
        v-for="node of treeNodes"
        :key="node.id"
        :node="node"
        :selected-id="selectedId"
        @selected="(id: number) => currentSelectedId = id"
    />
  </ul>
</template>

<style lang="scss">
.tree-folder-list{
  &__wrapper{
    text-align: left;
  }
}
</style>