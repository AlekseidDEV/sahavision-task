<script setup lang="ts">
import BaseBtn from "./components/ui/BaseBtn.vue";
import TreeFoldersModal from "./components/TreeFoldersModal.vue";

import {ref} from "vue";

const isShowModal = ref(false)
const treeFoldersData = [
  {
    id: 0, name: 'Папка 1', children: [
      {id: 3, name: 'Папка 1.1', children: []},
      {id: 4, name: 'Папка 1.2', children: []},
      {id: 5, name: 'Папка 1.3', children: []},
      {
        id: 6, name: 'Папка 1.4', children: [
          {id: 7, name: 'Папка 1.4.1', children: []},
          {id: 8, name: 'Папка 1.4.2', children: []},
          {
            id: 9, name: 'Папка 1.4.3', children: [
              {id: 13, name: 'Папка 1.4.3.1', children: []},
              {id: 14, name: 'Папка 1.4.3.1', children: []},
              {id: 15, name: 'Папка 1.4.3.1', children: []}
            ]
          },
        ]
      },
    ]
  },
  {
    id: 1, name: 'Папка 2', children: [
      {id: 10, name: 'Папка 1.4.1', children: []},
      {id: 11, name: 'Папка 1.4.2', children: []},
      {id: 12, name: 'Папка 1.4.3', children: []},
    ]
  },
  {id: 2, name: 'Папка 3', children: []}
]
</script>

<template>
  <div class="app__wrapper">
    <base-btn
        @click="isShowModal = true"
    >
      Открыть
    </base-btn>
    <tree-folders-modal
        v-model:show-modal="isShowModal"
        title="Tree Folders"
        :folder-data="treeFoldersData"
        @select="(id) => {console.log(id)}"
    />
  </div>
</template>

<style lang="scss">
.app {
  &__wrapper {
    position: relative;
  }
}
</style>
