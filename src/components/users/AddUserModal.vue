<template>
  <div
    v-if="isOpen"
    class="fixed inset-0 flex items-center justify-center bg-gray-800 bg-opacity-50 z-50"
  >
    <div class="bg-white p-6 rounded shadow-md w-96">
      <h2 class="text-lg font-bold mb-4">Add New User</h2>
      <form @submit.prevent="handleAddUser">
        <div class="mb-4">
          <label for="name" class="block text-sm font-medium mb-1">Name</label>
          <input
            v-model="userData.name"
            id="name"
            type="text"
            class="border px-4 py-2 w-full"
          />
        </div>
        <div class="mb-4">
          <label for="email" class="block text-sm font-medium mb-1"
            >Email</label
          >
          <input
            v-model="userData.email"
            id="email"
            type="email"
            class="border px-4 py-2 w-full"
          />
        </div>
        <div class="mb-4">
          <label for="status" class="block text-sm font-medium mb-1"
            >Status</label
          >
          <select
            v-model="userData.status"
            id="status"
            class="border px-4 py-2 w-full"
          >
            <option value="active">Active</option>
            <option value="inactive">Inactive</option>
          </select>
        </div>
        <button type="submit" class="bg-blue-500 text-white px-4 py-2 mr-2">
          Add
        </button>
        <button @click="closeModal" class="bg-gray-500 text-white px-4 py-2">
          Cancel
        </button>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref, defineEmits, defineProps } from "vue";

defineProps({
  isOpen: Boolean,
});

const emit = defineEmits(["close", "addUser"]);

const userData = ref({
  name: "",
  email: "",
  status: "active",
});

const closeModal = () => {
  emit("close");
};

const handleAddUser = () => {
  emit("addUser", userData.value);
  userData.value = { name: "", email: "", status: "active" };
  closeModal();
};
</script>

<style scoped>
/* Optional: Add additional styles if needed */
</style>
