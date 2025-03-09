<template>
  <div class="flex-1 p-6">
    <div class="flex justify-between items-center mb-4">
      <h2 class="text-xl font-semibold">{{ region }}</h2>
      <button
        @click="$emit('edit-region', region)"
        class="bg-gray-700 text-white px-3 py-1 rounded-none shadow-md hover:brightness-110"
      >
        Edit Region
      </button>
    </div>

    <button
      @click="$emit('add-client')"
      class="bg-gradient-to-r from-purple-600 to-blue-500 text-white px-4 py-2 mb-4 rounded-none shadow-md hover:brightness-110"
    >
      Create New Email Client
    </button>

    <ul>
      <li
        v-for="client in clients"
        :key="client.id"
        class="flex justify-between items-center bg-gray-800 p-2 mb-2 rounded-none"
      >
        {{ client.name }} - {{ client.email }}
        <div>
          <button
            @click="$emit('edit-client', client)"
            class="bg-blue-600 text-white px-3 py-1 rounded-none shadow-md hover:brightness-110"
          >
            Edit
          </button>
          <button
            @click="$emit('delete-client', client.id)"
            class="bg-red-600 text-white px-3 py-1 rounded-none shadow-md hover:brightness-110 ml-2"
          >
            Delete
          </button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { defineProps, computed } from "vue";
// defineProps(["region", "clients"]);
const props = defineProps({
  region: Object,
  clients: Array,
});
const clients = computed(() => props.clients);
</script>
