<script setup>
import { ref, onMounted } from 'vue'

const users = ref([])
const loading = ref(true)

const fetchUsers = async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/users')
    const data = await response.json()
    users.value = data
  } catch (error) {
    console.log('Error:', error)
  } finally {
    loading.value = false
  }
}

onMounted(() => {
  fetchUsers()
})
</script>

<template>
  <div class="container">
    <h1>Data Users</h1>

    <div v-if="loading" class="loading">Loading...</div>

    <div v-else class="list-container">
      <div v-for="user in users" :key="user.id" class="card">
        <div class="item">
          <label>Nama</label>
          <p class="name">{{ user.name }}</p>
        </div>
        
        <div class="item">
          <label>Email</label>
          <p class="email">{{ user.email }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
/* Background Full Layar Gelap */
.container {
  background-color: #121212;
  min-height: 100vh;
  padding: 40px 20px;
  color: white;
  font-family: sans-serif;
}

h1 {
  text-align: center;
  margin-bottom: 30px;
}

.loading {
  text-align: center;
}

/* Container untuk membungkus kotak-kotak ke bawah */
.list-container {
  display: flex;
  flex-direction: column;
  gap: 20px; /* Jarak antar kotak */
  max-width: 500px;
  margin: 0 auto;
}

/* Desain Kotak (Card) */
.card {
  background-color: #1e1e1e;
  padding: 20px;
  border-radius: 12px;
  border: 1px solid #333;
  box-shadow: 0 4px 6px rgba(0,0,0,0.3);
}

.item {
  margin-bottom: 10px;
}

.item label {
  display: block;
  font-size: 10px;
  text-transform: uppercase;
  color: #888;
  font-weight: bold;
  letter-spacing: 1px;
}

.name {
  font-size: 18px;
  font-weight: bold;
  margin: 5px 0;
}

.email {
  color: #3b82f6; /* Warna biru untuk email */
  font-size: 14px;
  margin: 0;
}
</style>