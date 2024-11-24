<script setup lang="ts">
import { type Folder } from "~/types/folder";

defineProps({
  isOpen: Boolean,
  title: String,
  folders: Array as () => Folder[],
});

const emit = defineEmits(["close", "select"]);

const selectedFolder = ref<number | null>(null);

const close = () => emit("close");
const confirm = () => {
  console.log("Selected Folder ID:", selectedFolder.value);
  if (selectedFolder.value) {
    emit("select", selectedFolder.value);
  }
  close();
};

const selectFolder = (id: number) => {
  console.log("Folder selected:", id);
  selectedFolder.value = id;
};
</script>
<template>
  <Dialog :open="isOpen" @close="close">
    <DialogContent>
      <DialogHeader>
        <DialogTitle>{{ title }}</DialogTitle>
      </DialogHeader>
      <DialogBody>
        <FolderTree :folders="folders" @select="selectFolder" />
      </DialogBody>
      <DialogFooter>
        <Button @click="close">Закрыть</Button>
        <Button @click="confirm">Ок</Button>
      </DialogFooter>
    </DialogContent>
  </Dialog>
</template>
