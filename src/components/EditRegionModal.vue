<template>
  <div
    class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50"
  >
    <div class="bg-gray-800 p-6 rounded-lg shadow-lg w-96">
      <h2 class="text-lg font-semibold mb-4">Edit Region</h2>
      <input
        v-model="editedRegion"
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
import { ref, defineProps, defineEmits } from "vue";

const props = defineProps(["region"]);
const emit = defineEmits(["close", "save"]);

const editedRegion = ref(props.region);

const save = () => {
  emit("save", editedRegion.value);
};
</script>
