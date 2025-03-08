<template>
  <div class="modal">
    <div class="modal-content">
      <h2>{{ editData ? "Edit" : "Create" }} Email Client</h2>
      <input v-model="email" placeholder="Email" />
      <input v-model="name" placeholder="Name" />
      <input v-model="origin" placeholder="Origin" />
      <input v-model="destination" placeholder="Destination" />
      <div>
        <label v-for="state in states" :key="state">
          <input type="checkbox" v-model="selectedStates" :value="state" />
          {{ state }}
        </label>
      </div>
      <button @click="save">Save</button>
      <button @click="$emit('close')">Cancel</button>
    </div>
  </div>
</template>

<script setup>
import { ref, watch } from "vue";

const props = defineProps(["editData"]);
const emit = defineEmits(["close", "save"]);

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

const save = () => {
  emit("save", {
    id: props.editData?.id || Date.now(),
    email: email.value,
    name: name.value,
    origin: origin.value,
    destination: destination.value,
    states: selectedStates.value,
  });
};
</script>
