<template>
  <div class="sidebar">
    <button @click="$emit('add-region')">Create Region</button>
    <ul>
      <li
        v-for="region in regions"
        :key="region"
        @click="$emit('select-region', region)"
      >
        {{ region }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ["regions"],
};
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
