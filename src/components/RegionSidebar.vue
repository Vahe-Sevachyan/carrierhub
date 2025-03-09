<template>
  <div class="w-64 bg-gray-800 p-4">
    <button
      @click="$emit('add-region')"
      class="w-full bg-gradient-to-r from-purple-600 to-blue-500 text-white py-2 mb-4 rounded-none shadow-md hover:brightness-110"
    >
      Create Region
    </button>
    <ul>
      <li
        v-for="region in regions"
        :key="region"
        class="relative group cursor-pointer p-2 bg-gray-700 rounded-none hover:bg-gray-600 transition flex justify-between items-center"
        @click="$emit('select-region', region)"
      >
        <span>{{ region }}</span>
        <span
          @click.stop="$emit('edit-region', region)"
          class="absolute right-2 text-gray-400 opacity-0 group-hover:opacity-100 hover:text-white cursor-pointer transition"
        >
          ✏️
        </span>
      </li>
    </ul>
  </div>
</template>

<script setup>
defineProps(["regions"]);
</script>

<style>
.sidebar {
  width: 250px;
  background: #333;
  color: white;
  padding: 10px;
}
button {
  width: 100%;
  margin-bottom: 10px;
}
ul {
  list-style: none;
  padding: 0;
}
li {
  cursor: pointer;
  padding: 5px;
}
</style>
