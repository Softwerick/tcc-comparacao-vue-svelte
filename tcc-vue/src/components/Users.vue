<template>
    <div>
      <h1>Meus Dados</h1>
      <div class="user-grid">
        <div class="user" v-for="user in jsonData.users" :key="user.id">
		      <p>{{ user.name }} - {{ user.occupation }}</p>
          <img src="/teste.jpg" width="300"/>
          <button @click="deleteItem(user.id)">Deletar</button>
		    </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        jsonData: []
      };
    },
    mounted() {
      this.loadData();
    },
    methods: {
      async loadData() {
        try {
          const response = await fetch('/data.json');
          if (!response.ok) {
            throw new Error('Failed to fetch');
          }
          this.jsonData = await response.json();
        } catch (error) {
          console.error('Error loading data:', error);
        }
      },

      async deleteItem(userId) {
        try {
          // Simula a remoção localmente
          const updatedUsers = this.jsonData.users.filter(user => user.id !== userId);
          localStorage.setItem('users', JSON.stringify(updatedUsers));
          
          this.jsonData.users = updatedUsers

        } catch (error) {
          console.error('Error deleting item:', error);
        }
    }
    }
  };
  </script>
  