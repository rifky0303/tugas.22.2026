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
        <p class="name">{{ user.name }}</p>
        <p class="email">{{ user.email }}</p>
        <a href="#" class="read-more">Read more &rarr;</a>
      </div>
    </div>
  </div>
</template>

<style scoped>
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

.list-container {
  max-width: 500px;
  margin: 0 auto;
  border-top: 1px solid #333;
}

.card {
  background-color: transparent;
  padding: 30px 20px;
  text-align: center;
  
  /* Hanya gunakan border samping dan bawah agar tidak double */
  border-left: 1px solid #333;
  border-right: 1px solid #333;
  border-bottom: 1px solid #333;
  
  /* Menghilangkan margin agar kotak menempel */
  margin-bottom: 0; 
}

.name {
  font-size: 22px;
  font-weight: 600;
  color: #e2e8f0;
  margin: 0 0 5px 0;
}

.email {
  color: #94a3b8;
  font-size: 15px;
  margin: 0 0 15px 0;
}

.read-more {
  display: inline-block;
  color: #ffffff;
  text-decoration: none;
  font-size: 14px;
  font-weight: bold;
}

.read-more:hover {
  text-decoration: underline;
}
</style>