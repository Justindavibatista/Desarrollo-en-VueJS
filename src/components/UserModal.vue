<template>
  <div class="app-container">
    <header class="header">
      <h1>Lista de Usuarios</h1>
    </header>

    <div class="content">
      <ul class="user-list">
        <li v-for="user in users" :key="user.id" @click="selectUser(user)">
          {{ user.name }}
        </li>
      </ul>
    </div>

    <div v-if="selectedUser" class="modal-overlay" @click.self="closeModal">
      <div class="modal">
        <h2>{{ selectedUser.name }}</h2>
        <p><strong>Email:</strong> {{ selectedUser.email }}</p>
        <p><strong>Dirección:</strong> {{ selectedUser.address.street }}, {{ selectedUser.address.city }}</p>
        <button @click="closeModal">Cerrar</button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      users: [],
      selectedUser: null,
    };
  },
  mounted() {
    this.fetchUsers();
  },
  methods: {
    async fetchUsers() {
      try {
        const response = await axios.get("https://jsonplaceholder.typicode.com/users");
        this.users = response.data;
      } catch (error) {
        console.error("Error fetching users:", error);
      }
    },
    selectUser(user) {
      this.selectedUser = user;
    },
    closeModal() {
      this.selectedUser = null;
    },
  },
};
</script>

<style scoped>

.app-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  background-image: url('@/assets/usuarios.jpg'); 
  background-size: cover;
  background-position: center;
  padding: 20px;
  box-sizing: border-box;
}


.header {
  width: 100%;
  max-width: 1200px;
  text-align: center;
  margin-bottom: 20px;
}

.header h1 {
  font-size: 2.5em;
  color: #2c3e50;
  margin: 0;
  padding: 10px 20px;
  background-color: rgba(255, 255, 255, 0.8);
  border-radius: 8px;
  font-weight: bold;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}


.content {
  display: flex;
  justify-content: center;
  width: 100%;
  max-width: 1200px;
}

.user-list {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  gap: 15px;
  padding: 0;
  width: 100%;
}

.user-list li {
  background-color: rgba(227, 242, 253, 0.8);
  color: #333;
  font-weight: 500;
  padding: 15px;
  border-radius: 8px;
  text-align: center;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.user-list li:hover {
  background-color: #bbdefb;
}


.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal {
  background: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
  width: 90%;
  max-width: 400px;
}


button {
  margin-top: 15px;
  padding: 8px 12px;
  background-color: #2196f3;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #1976d2;
}
</style>
