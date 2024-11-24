<script setup lang="ts">
import { type Folder } from "~/types/folder";

const mockFolders: Folder[] = [
  {
    id: 1,
    name: "Папка 1",
    children: [
      { id: 2, name: "Папка 1.1", children: [] },
      {
        id: 3,
        name: "Папка 1.2",
        children: [{ id: 4, name: "Папка 1.2.1", children: [] }],
      },
    ],
  },
  { id: 5, name: "Папка 2", children: [] },
];

const isModalOpen = ref(false);

const openModal = () => (isModalOpen.value = true);
const closeModal = () => (isModalOpen.value = false);

const handleSelect = (folderId: number) => {
  console.log("Selected folder ID:", folderId);
};
</script>
<template>
  <Header />
  <div>
    <Button class="m-5 w-40 h-20 text-3xl" @click="openModal">Открыть</Button>
    <ModalDialog
      v-if="isModalOpen"
      :isOpen="isModalOpen"
      :title="'Выберите папку'"
      :folders="mockFolders"
      @close="closeModal"
      @select="handleSelect"
    />
  </div>
</template>
