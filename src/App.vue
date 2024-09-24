<template>
  <div class="flex">
    <div class="bg-gray-800 text-white w-64 space-y-6 py-7 px-2">
      <h1 class="text-xl font-bold">Dashboard</h1>
      <nav>
        <a href="#" class="block py-2.5 px-4 rounded hover:bg-gray-700"
          >Users</a
        >
        <a href="#" class="block py-2.5 px-4 rounded hover:bg-gray-700"
          >Reports</a
        >
        <!-- Add more links as needed -->
      </nav>
    </div>

    <div class="flex-1 p-10">
      <div class="bg-white p-5 rounded-lg shadow">
        <h2 class="text-lg font-semibold">Statistics</h2>
        <p>Registered Users: <span id="userCount">0</span></p>
        <p>Active Requests: <span id="activeRequests">0</span></p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
