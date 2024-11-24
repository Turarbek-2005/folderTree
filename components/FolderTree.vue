<template>
  <ul>
    <li class="ml-4" v-for="folder in folders" :key="folder.id">
      <div
        @click="
          () => {
            select(folder.id);
            toggle(folder.id);
          }
        "
        class="mb-2"
      >
        <Button :class="{ selected: folder.id === selected }">{{
          folder.name
        }}</Button>
      </div>
      <FolderTree
        v-if="isOpen(folder.id)"
        :folders="folder.children"
        @select="select"
      />
    </li>
  </ul>
</template>

<script setup lang="ts">
import { type Folder } from "~/types/folder";

defineProps({
  folders: Array as () => Folder[],
});

const emit = defineEmits(["select"]);

const openFolders = ref<Set<number>>(new Set());
const selected = ref<number | null>(null);

const toggle = (id: number) => {
  if (openFolders.value.has(id)) openFolders.value.delete(id);
  else openFolders.value.add(id);
};

const isOpen = (id: number) => openFolders.value.has(id);

const select = (id: number) => {
  console.log("Tree selection:", id);
  selected.value = id;
  emit("select", id);
};
</script>

<style scoped>
.selected {
  color: black;
}
</style>
