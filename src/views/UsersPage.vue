<template>
    <div class="w-100 overflow-auto">
      <h1 class="text-2xl font-semibold mb-4">User Management</h1>
  
      <button
        @click="openAddModal"
        class="bg-green-500 text-white px-4 py-2 mb-4"
      >
        Add New User
      </button>
  
      <!-- Search & Filter -->
      <div class="flex items-center mb-4 flex-wrap">
        <input
          v-model="searchQuery"
          type="text"
          class="border p-2 rounded mr-4"
          placeholder="Search users..."
        />
        <select v-model="filterStatus" class="border p-2 rounded">
          <option value="">All</option>
          <option value="active">Active</option>
          <option value="inactive">Inactive</option>
        </select>
      </div>
  
      <!-- User Table -->
      <table class="table-auto w-full bg-white shadow-md rounded">
        <thead class="bg-gray-200">
          <tr>
            <th class="px-4 py-2">Name</th>
            <th class="px-4 py-2">Email</th>
            <th class="px-4 py-2">Status</th>
            <th class="px-4 py-2">Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="user in filteredUsers" :key="user.id" class="border-t">
            <td class="px-4 py-2">{{ user.name }}</td>
            <td class="px-4 py-2">{{ user.email }}</td>
            <td class="px-4 py-2">{{ user.status }}</td>
            <td class="px-4 py-2">
              <button class="text-blue-500 mr-2" @click="openEditModal(user)">
                Edit
              </button>
              <button class="text-red-500" @click="openDeleteModal(user)">
                Delete
              </button>
            </td>
          </tr>
        </tbody>
      </table>
  
      <AddUserModal
        :isOpen="isAddModalOpen"
        @close="closeAddModal"
        @addUser="addUser"
      />
  
      <EditUserModal
        :isOpen="isEditModalOpen"
        :user="selectedUser"
        @close="closeEditModal"
        @updateUser="updateUser"
      />
  
      <DeleteUserModal
        :isOpen="isDeleteModalOpen"
        :user="selectedUser"
        @close="closeDeleteModal"
        @confirmDelete="confirmDeleteUser"
      />
    </div>
  </template>
  
  <script setup>
  import { ref, computed, onMounted } from "vue";
  import axios from "axios";
  import AddUserModal from "../components/users/AddUserModal";
  import EditUserModal from "../components/users/EditUserModal";
  import DeleteUserModal from "../components/users/DeleteUserModal";
  
  const users = ref([]);
  const searchQuery = ref("");
  const filterStatus = ref("");
  const isAddModalOpen = ref(false);
  const isEditModalOpen = ref(false);
  const isDeleteModalOpen = ref(false);
  const selectedUser = ref(null);
  
  onMounted(async () => {
    const response = await axios.get(
      "https://jsonplaceholder.typicode.com/users"
    );
    users.value = response.data.map((user) => ({
      ...user,
      status: Math.random() > 0.5 ? "active" : "inactive", // assign some random status to the users data
    }));
  });
  
  const filteredUsers = computed(() => {
    let filtered = users.value;
  
    if (searchQuery.value) {
      filtered = filtered.filter((user) =>
        user.name.toLowerCase().includes(searchQuery.value.toLowerCase())
      );
    }
  
    if (filterStatus.value) {
      filtered = filtered.filter((user) => user.status === filterStatus.value);
    }
  
    return filtered;
  });
  
  const openAddModal = () => {
    isAddModalOpen.value = true;
  };
  const closeAddModal = () => {
    isAddModalOpen.value = false;
  };
  
  const openEditModal = (user) => {
    selectedUser.value = user;
    isEditModalOpen.value = true;
  };
  const closeEditModal = () => {
    isEditModalOpen.value = false;
    selectedUser.value = null;
  };
  
  const openDeleteModal = (user) => {
    isDeleteModalOpen.value = true;
    selectedUser.value = user;
  };
  const closeDeleteModal = () => {
    isDeleteModalOpen.value = false;
    selectedUser.value = null;
  };
  
  // Add new user to the list
  const addUser = (newUser) => {
    fetch("https://jsonplaceholder.typicode.com/users", {
      method: "POST",
      body: JSON.stringify({ ...newUser, id: users.value.length + 1 }),
      headers: {
        "Content-type": "application/json; charset=UTF-8",
      },
    })
      .then((response) => response.json())
      .then(() => {
        users.value.push({ ...newUser, id: users.value.length + 1 });
  
        setTimeout(() => {
          window.alert("User is added successfully!");
        }, 10);
      })
      .catch((e) => {
        console.error({ e });
        window.alert("something went wrong!");
      });
  };
  
  const updateUser = (updatedUser) => {
    fetch("https://jsonplaceholder.typicode.com/users/" + updatedUser.id, {
      method: "PATCH",
      body: JSON.stringify({ ...updatedUser }),
      headers: {
        "Content-type": "application/json; charset=UTF-8",
      },
    })
      .then((response) => response.json())
      .then(() => {
        const index = users.value.findIndex((u) => u.id === updatedUser.id);
  
        if (index !== -1) {
          users.value[index] = updatedUser;
  
          setTimeout(() => {
            window.alert("User is edited successfully!");
          }, 10);
        }
      })
      .catch((e) => {
        console.error({ e });
        window.alert("something went wrong!");
      });
  };
  
  const confirmDeleteUser = (user) => {
    fetch("https://jsonplaceholder.typicode.com/users/" + user.id, {
      method: "DELETE",
    }).then((res) => {
      console.log(res);
      if (res.ok) {
        users.value = users.value.filter((u) => u.id !== user.id);
  
        setTimeout(() => {
          window.alert("User is deleted successfully!");
        }, 10);
      }
    });
  };
  </script>
  