<script>
export default {
  data() {
    return { user: null, loading: true, error: '' }
  },
  async mounted() {
    try {
      const response = await fetch('https://dummyjson.com/auth/me', {
        method: 'GET',
        headers: { Authorization: 'Bearer ' + localStorage.getItem('token') },
      })
      const data = await response.json()
      if (!response.ok) {
        throw new Error(data.message || 'Failed to load profile')
      }
      this.user = data
    } catch (error) {
      this.error = error.message
    } finally {
      this.loading = false
    }
  },
}
</script>

<template>
  <section class="profile-page">
    <h1 v-if="error" class="error" role="alert">{{ error }}</h1>
    <h1 v-else>My profile</h1>
    <p v-if="loading" role="status">Loading profile...</p>
    <div v-else-if="user" class="profile-content">
      <div class="profile-details">
        <p>Username: {{ user.username }}</p>
        <p>Name: {{ user.firstName }}</p>
        <p>Lastname: {{ user.lastName }}</p>
        <p>Gender: {{ user.gender }}</p>
        <p>Email: {{ user.email }}</p>
      </div>
      <img class="profile-image" :src="user.image" :alt="user.firstName + ' ' + user.lastName" />
    </div>
  </section>
</template>
