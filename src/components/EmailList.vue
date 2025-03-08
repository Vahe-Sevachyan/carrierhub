<template>
  <div class="email-list">
    <h2>{{ region }}</h2>
    <button @click="$emit('add-client')">Create New Email Client</button>
    <ul>
      <li v-for="client in clients" :key="client.id">
        {{ client.name }} - {{ client.email }}
        <button @click="$emit('edit-client', client)">Edit</button>
        <button @click="$emit('delete-client', client.id)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
defineProps(["region", "clients"]);
</script>
