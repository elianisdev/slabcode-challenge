<script setup lang="ts">
import Calendar from "./components/Calendar.vue";
import NewReminder from "./views/NewReminder.vue";
import {useModalStore} from "./stores/modal.ts";

const modalStore = useModalStore();

const openModal = () => {
  modalStore.openModal();
}

</script>

<template>

  <div class="container">
    <h1>SlabCode Challenge</h1>
    <p> This challenge manage personal reminders in a Calendar view</p>

    <div>
      <button class="btn btn-primary" @click="openModal">Add new reminder</button>
    </div>

    <calendar />

    <new-reminder />

  </div>
</template>

<style scoped>

</style>
