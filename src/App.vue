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
    console.error('Error:', error)
  } finally {
    loading.value = false
  }
}

onMounted(() => {
  fetchUsers()
})
</script>

<template>
  <div class="main-container py-5">
    <div class="container">
      <h1 class="text-center mb-5 title-data">Data User</h1>

      <div v-if="loading" class="text-center">
        <div class="spinner-border text-danger" role="status"></div>
        <p>Loading...</p>
      </div>

      <div v-else class="row row-cols-1 row-cols-md-2 g-4">
        <div v-for="user in users" :key="user.id" class="col">
          
          <div class="custom-card">
            <h5 class="user-name">{{ user.name }}</h5>
            <p class="user-email">{{ user.email }}</p>
          </div>

        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.main-container {
  background-color: #f1f5f9; /* Warna background layar */
  min-height: 100vh;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.title-data {
  color: #475569;
  font-weight: bold;
}

/* Styling kartu agar mirip dengan gambar yang kamu kirim */
.custom-card {
  background-color: white;
  border: 2px solid #fbcfe8; /* Border Pink Muda */
  border-radius: 15px;       /* Membuat sudut melengkung */
  padding: 20px;
  text-align: center;
  transition: all 0.3s ease;
}

.custom-card:hover {
  border-color: #f472b6; /* Pink lebih gelap saat di-hover */
  transform: translateY(-2px);
}

.user-name {
  font-weight: 700;
  color: #334155;
  margin-bottom: 5px;
}

.user-email {
  color: #64748b;
  font-size: 0.9rem;
  margin-bottom: 0;
}
</style>