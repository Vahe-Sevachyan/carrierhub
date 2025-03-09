<template>
  <div
    class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50"
  >
    <div class="bg-gray-800 p-6 rounded-lg shadow-lg w-96">
      <h2 class="text-lg font-semibold mb-4">
        {{ editData ? "Edit" : "Create" }} Email Client
      </h2>
      <input
        v-model="email"
        placeholder="Email"
        class="w-full p-2 bg-gray-700 text-white rounded-none mb-2"
      />
      <input
        v-model="name"
        placeholder="Name"
        class="w-full p-2 bg-gray-700 text-white rounded-none mb-2"
      />
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
      <div class="grid grid-cols-3 gap-2 mb-4">
        <label v-for="state in states" :key="state" class="flex items-center">
          <input
            type="checkbox"
            v-model="selectedStates"
            :value="state"
            class="mr-2"
          />
          {{ state }}
        </label>
      </div>
      <div class="flex justify-between">
        <button
          @click="saveClient"
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
import { ref, watch } from "vue";

const props = defineProps(["editData"]);
const emit = defineEmits(["close", "save-client"]);

const email = ref("");
const name = ref("");
const origin = ref("");
const destination = ref("");
const selectedStates = ref([]);
const states = ["CA", "NY", "AZ", "WI"];

watch(
  () => props.editData,
  (data) => {
    if (data) {
      email.value = data.email;
      name.value = data.name;
      origin.value = data.origin;
      destination.value = data.destination;
      selectedStates.value = data.states || [];
    }
  },
  { immediate: true }
);

const saveClient = () => {
  if (!email.value || !name.value) return; // ✅ Prevent empty submissions

  // Emitting newClient object correctly
  emit("save-client", {
    id: Date.now(), // ✅ Unique ID
    email: email.value,
    name: name.value,
    origin: origin.value,
    destination: destination.value,
    states: selectedStates.value,
  });

  // ✅ Clear form after saving
  email.value = "";
  name.value = "";
  origin.value = "";
  destination.value = "";
  selectedStates.value = [];

  emit("close"); // ✅ Close modal after saving
};
</script>
