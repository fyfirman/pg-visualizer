<script setup lang="ts">
import { ref } from "vue";
import PevVue from '../components/Pev.vue';
import Button from 'primevue/button';
import Dialog from 'primevue/dialog';

const visible = ref(false);


function toggleVisible() {
  visible.value = !visible.value;
}
</script>

<template>
  <main>
    <Button label="Show" @click="toggleVisible" />
    <PevVue />
    <Dialog
      v-model:visible="visible"
      modal
      header="Edit Plan"
      :style="{ width: '80vw' }"
    >
      <p>Edit query modal</p>
    </Dialog>
  </main>
</template>
