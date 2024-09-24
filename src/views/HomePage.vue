<template>
  <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4">
    <div class="bg-white p-6 rounded-lg shadow-md">
      <h3 class="text-xl font-semibold mb-4">Total Users</h3>
      <p class="text-4xl">{{ totalUsers }}</p>
    </div>
    <div class="bg-white p-6 rounded-lg shadow-md">
      <h3 class="text-xl font-semibold mb-4">Active Orders</h3>
      <p class="text-4xl">152</p>
    </div>
    <div class="bg-white p-6 rounded-lg shadow-md">
      <h3 class="text-xl font-semibold mb-4">New Users Today</h3>
      <p class="text-4xl">5</p>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";

const totalUsers = ref(0);

onMounted(async () => {
  const response = await axios.get(
    "https://jsonplaceholder.typicode.com/users"
  );
  totalUsers.value = response.data.length;
});
</script>
