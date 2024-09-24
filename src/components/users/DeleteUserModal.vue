<template>
  <div
    v-if="isOpen"
    class="fixed inset-0 flex items-center justify-center bg-gray-800 bg-opacity-50 z-50"
  >
    <div class="bg-white p-6 rounded shadow-md w-96">
      <h2 class="text-lg font-bold mb-4">Delete User</h2>
      <p>
        Are you sure you want to delete the user <strong>{{ user.name }}</strong
        >?
      </p>
      <div class="mt-6 flex justify-end">
        <button
          @click="deleteUser"
          class="bg-red-500 text-white px-4 py-2 mr-2"
        >
          Delete
        </button>
        <button @click="closeModal" class="bg-gray-500 text-white px-4 py-2">
          Cancel
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from "vue";

const props = defineProps({
  isOpen: Boolean,
  user: Object, // User to be deleted (pass name and other necessary info)
});

const emit = defineEmits(["close", "confirmDelete"]);

const closeModal = () => {
  emit("close");
};

const deleteUser = () => {
  emit("confirmDelete", props.user);
  closeModal();
};
</script>

<style scoped>
/* Optional: Add additional styles if needed */
</style>
