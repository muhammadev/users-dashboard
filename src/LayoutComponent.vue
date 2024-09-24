<template>
  <div class="flex w-full min-h-screen bg-gray-100">
    <!-- Sidebar -->
    <aside
      :class="[
        'bg-white shadow-md transform transition-transform duration-300 ease-in-out',
        isSidebarOpen ? 'translate-x-0' : '-translate-x-full',
        'fixed z-30 inset-y-0 left-0 w-64 md:relative md:translate-x-0',
      ]"
    >
      <div class="p-6">
        <h2 class="text-lg font-semibold">Dashboard</h2>
      </div>
      <nav>
        <ul>
          <li class="py-2 px-4 hover:bg-gray-200">
            <router-link to="/">Home</router-link>
          </li>
          <li class="py-2 px-4 hover:bg-gray-200">
            <router-link to="/users">Users</router-link>
          </li>
        </ul>
      </nav>
    </aside>

    <!-- Main content -->
    <div class="flex flex-col flex-grow w-full overflow-hidden">
      <!-- Top bar -->
      <header class="bg-white shadow p-4 flex justify-between items-center">
        <button
          @click="toggleSidebar"
          class="text-gray-500 hover:text-gray-700 inline-block md:invisible"
        >
          <img class="w-6 h-6" src="@/assets/menu.svg" alt="" />
        </button>
        <div class="flex items-center space-x-4">
          <span>{{ user.name }}</span>
          <!-- TODO: notifications button -->
          <button class="relative text-gray-500 hover:text-gray-700">
            <img class="w-6 h-6" src="@/assets/bell.svg" alt="" />
          </button>
        </div>
      </header>

      <!-- Main page content -->
      <main class="w-100 p-6 overflow-hidden">
        <router-view></router-view>
      </main>
    </div>

    <!-- Backdrop overlay for small screens when sidebar is open -->
    <div
      v-if="isSidebarOpen"
      @click="toggleSidebar"
      class="w-screen h-screen fixed inset-0 bg-black bg-opacity-50 z-20 md:hidden"
    ></div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

const isSidebarOpen = ref(false);
const user = ref({ name: "Mohamed" });

function toggleSidebar() {
  isSidebarOpen.value = !isSidebarOpen.value;
}

onMounted(() => {});
</script>

<style scoped>
/* @media (min-width: 768px) {
  .w-64 {
    display: block !important;
  }
} */
</style>
