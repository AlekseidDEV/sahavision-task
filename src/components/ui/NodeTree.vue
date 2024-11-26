<script setup lang="ts">
import {IntTreeFolderList} from "../../model/treeFolderList.ts";

import {computed, ref} from "vue";

const props = defineProps<{
  node: IntTreeFolderList,
  selectedId: number | null | undefined
}>()

const emits = defineEmits<{
  (e: 'selected', id: number): void
}>()

const showNode = ref(false)

const hasNodeChildren = computed(() => {
  return props.node.children.length !== 0
})

const toggleList = (id: number) => {
  showNode.value = !showNode.value
  emits("selected", id)
}

</script>

<template>
  <li
      class="node-tree__wrapper"
      @click="toggleList(node.id)"
  >
    <div :class="selectedId === node.id ? 'node-tree--selected' : ''">
      <span>
        {{ node.name }}
      </span>
      <span v-if="hasNodeChildren">---</span>
    </div>
  </li>
  <div v-if="hasNodeChildren && showNode">
    <ul>
      <node-tree
          v-for="child of node.children"
          :node="child"
          :selected-id="selectedId"
          @selected="(id) => emits('selected', id)"
      />
    </ul>
  </div>
</template>

<style lang="scss">
.node-tree{
  &__wrapper{
    cursor: pointer;
  }
  &--selected{
    background: grey;
    border-radius: 4px;
    padding: 2px;
  }
}
</style>