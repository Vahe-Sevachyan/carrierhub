<template>
  <div class="flex h-screen bg-gray-900 text-white">
    <RegionSidebar
      :regions="regions"
      @add-region="showRegionModal = true"
      @edit-region="editRegion"
      @select-region="selectRegion"
    />

    <EmailList
      v-if="selectedRegion"
      :region="selectedRegion"
      :clients="emailClients[selectedRegion] || []"
      @add-client="showEmailModal = true"
      @edit-client="editClient"
      @delete-client="deleteClient"
      @edit-region="editRegion"
    />

    <RegionModal
      v-if="showRegionModal"
      @close="showRegionModal = false"
      @save="addRegion"
    />

    <EmailModal
      v-if="showEmailModal"
      @close="showEmailModal = false"
      @save-client="saveClient"
      :editData="editClientData"
    />
    <EditRegionModal
      v-if="showEditRegionModal"
      @close="showEditRegionModal = false"
      @save="updateRegion"
      :region="regionToEdit"
    />
  </div>
</template>

<script setup>
import "./main.css";
import { ref } from "vue";
import RegionSidebar from "./components/RegionSidebar.vue";
import RegionModal from "./components/RegionModal.vue";
import EmailList from "./components/EmailList.vue";
import EmailModal from "./components/EmailModal.vue";
import EditRegionModal from "./components/EditRegionModal.vue";

const regions = ref([]);
const selectedRegion = ref(null);
const showRegionModal = ref(false);
const showEmailModal = ref(false);
const showEditRegionModal = ref(false);
const regionToEdit = ref(null);
const emailClients = ref({});
const editClientData = ref(null);

const addRegion = (region) => {
  regions.value.push(region);
  emailClients.value[region.id] = []; // Ensure to use region.id
  showRegionModal.value = false;
};

const selectRegion = (region) => {
  selectedRegion.value = region;
};

const editRegion = (region) => {
  regionToEdit.value = region;
  showEditRegionModal.value = true;
};

const editClient = (client) => {
  editClientData.value = client;
  showEmailModal.value = true; // Open the email modal for editing
};
const deleteClient = (clientId) => {
  const regionClients = emailClients.value[selectedRegion.value];
  const index = regionClients.findIndex((client) => client.id === clientId);
  if (index !== -1) {
    regionClients.splice(index, 1); // Remove the client from the array
  }
};
const saveClient = (newClient) => {
  if (!emailClients.value[selectedRegion.value]) {
    emailClients.value[selectedRegion.value] = [];
  }

  if (editClientData.value) {
    const index = emailClients.value[selectedRegion.value].findIndex(
      (c) => c.id === newClient.id // Use newClient instead of client
    );
    emailClients.value[selectedRegion.value][index] = newClient; // Correctly reference newClient
  } else {
    newClient.id = Date.now(); // Use newClient for id assignment
    emailClients.value[selectedRegion.value].push(newClient); // Push the new client
  }

  showEmailModal.value = false;
  editClientData.value = null;
};

const updateRegion = (updatedRegion) => {
  const index = regions.value.indexOf(regionToEdit.value);
  if (index !== -1) {
    regions.value[index] = updatedRegion;

    // Update selected region if it was renamed
    if (selectedRegion.value === regionToEdit.value) {
      selectedRegion.value = updatedRegion;
    }

    // Preserve email clients under the renamed region
    emailClients.value[updatedRegion] = emailClients.value[regionToEdit.value];
    delete emailClients.value[regionToEdit.value];
  }
  showEditRegionModal.value = false;
};
</script>

<style></style>
