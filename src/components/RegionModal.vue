<template>
  <div class="modal">
    <div class="modal-content">
      <h2>Create Region</h2>
      <input v-model="origin" placeholder="Origin" />
      <input v-model="destination" placeholder="Destination" />
      <button @click="save">Save</button>
      <button @click="$emit('close')">Cancel</button>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const origin = ref("");
const destination = ref("");
const emit = defineEmits(["close", "save"]);

const save = () => {
  if (origin.value && destination.value) {
    emit("save", `${origin.value} - ${destination.value}`);
  }
};
</script>

<style>
.modal {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}
.modal-content {
  background: white;
  padding: 20px;
  border-radius: 5px;
}
</style>
