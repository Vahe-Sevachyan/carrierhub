<template>
  <div
    class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50"
  >
    <div class="bg-gray-800 p-6 rounded-lg shadow-lg w-96">
      <h2 class="text-lg font-semibold mb-4">Create Region</h2>
      <input
        v-model="origin"
        placeholder="Origin"
        class="w-full p-2 bg-gray-700 text-white rounded-none mb-2"
      />
      <input
        v-model="destination"
        placeholder="Destination"
        class="w-full p-2 bg-gray-700 text-white rounded-none mb-4"
      />
      <div class="flex justify-between">
        <button
          @click="save"
          class="bg-purple-600 hover:brightness-110 text-white px-4 py-2 rounded-none shadow-md"
        >
          Save
        </button>
        <button
          @click="$emit('close')"
          class="bg-gray-600 hover:brightness-110 text-white px-4 py-2 rounded-none shadow-md"
        >
          Cancel
        </button>
      </div>
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
