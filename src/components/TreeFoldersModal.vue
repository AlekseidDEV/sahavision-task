<script setup lang="ts">
import BaseBtn from "./ui/BaseBtn.vue";
import TreeFolderList from "./TreeFolderList.vue";

import {IntTreeFolderList} from "../model/treeFolderList.ts";
import {Ref, ref} from "vue";

defineProps<{
  title?: string,
  folderData: IntTreeFolderList[]
}>()

const emits = defineEmits<{
  (e: 'select', id: number | null): void
}>()

const model = defineModel<boolean>('showModal')

const currentFolderId: Ref<null | number> = ref(null)

const saveSelectedFolder = () => {
  model.value = false
  emits('select', currentFolderId.value)
}

</script>

<template>
  <div
      v-if="model"
      class="tree-folders-modal__wrapper"
  >
    <div class="tree-folders-modal__content">
      <h2>
        {{ title }}
      </h2>
      <div class="tree-folders-modal__folders-list">
        <tree-folder-list
            v-model:selected-id="currentFolderId"
            :tree-nodes="folderData"
        />
      </div>
      <div class="tree-folders-modal__btns">
        <base-btn
            color-btn="green"
            @click="saveSelectedFolder"
        >
          Ок
        </base-btn>
        <base-btn
            color-btn="green"
            @click="model = false"
        >
          Закрыть
        </base-btn>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
.tree-folders-modal {
  &__wrapper {
    position: fixed;
    background: rgba(81, 81, 81, 0.22);
    width: 100%;
    height: 100vh;
    top: 0;
    left: 0;
  }
  &__content {
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    position: absolute;
    position: fixed;
    background-color: #1a1a1a;
    padding: 20px 50px;
    border-radius: 8px;
  }
  &__btns{
    display: flex;
    gap: 20px;
    button {
      width: 130px;
    }
  }
  &__folders-list{
    margin-bottom: 40px;
    text-align: left;
  }
}
</style>