<template>
  <div class="app-container">
    <RegionSidebar
      :regions="regions"
      @add-region="showRegionModal = true"
      @select-region="selectRegion"
    />
    <EmailList
      v-if="selectedRegion"
      :region="selectedRegion"
      :clients="emailClients[selectedRegion] || []"
      @add-client="showEmailModal = true"
      @edit-client="editClient"
      @delete-client="deleteClient"
    />

    <RegionModal
      v-if="showRegionModal"
      @close="showRegionModal = false"
      @save="addRegion"
    />
    <EmailModal
      v-if="showEmailModal"
      @close="showEmailModal = false"
      @save="saveClient"
      :editData="editClientData"
    />
  </div>
</template>

<script setup>
import { ref } from "vue";
import RegionSidebar from "./components/RegionSidebar.vue";
import RegionModal from "./components/RegionModal.vue";
import EmailList from "./components/EmailList.vue";
import EmailModal from "./components/EmailModal.vue";

const regions = ref([]);
const selectedRegion = ref(null);
const showRegionModal = ref(false);
const showEmailModal = ref(false);
const emailClients = ref({});
const editClientData = ref(null);

const addRegion = (region) => {
  regions.value.push(region);
  emailClients.value[region] = [];
  showRegionModal.value = false;
};

const selectRegion = (region) => {
  selectedRegion.value = region;
};

const editClient = (client) => {
  editClientData.value = client;
  showEmailModal.value = true;
};

const saveClient = (client) => {
  if (!emailClients.value[selectedRegion.value]) {
    emailClients.value[selectedRegion.value] = [];
  }
  if (editClientData.value) {
    const index = emailClients.value[selectedRegion.value].findIndex(
      (c) => c.id === client.id
    );
    emailClients.value[selectedRegion.value][index] = client;
  } else {
    client.id = Date.now();
    emailClients.value[selectedRegion.value].push(client);
  }
  showEmailModal.value = false;
  editClientData.value = null;
};

const deleteClient = (clientId) => {
  emailClients.value[selectedRegion.value] = emailClients.value[
    selectedRegion.value
  ].filter((c) => c.id !== clientId);
};
</script>

<style>
.app-container {
  display: flex;
}
</style>
