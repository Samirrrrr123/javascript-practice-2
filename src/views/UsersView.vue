<script>
export default {
  data() {
    return { users: [], loading: true, error: '' }
  },
  async mounted() {
    try {
      const response = await fetch('https://dummyjson.com/users')
      const data = await response.json()
      if (!response.ok) {
        throw new Error(data.message || 'Failed to load users')
      }
      this.users = data.users
    } catch (error) {
      this.error = error.message
    } finally {
      this.loading = false
    }
  },
}
</script>

<template>
  <section class="users-page" aria-label="Users">
    <p v-if="loading" role="status">Loading users...</p>
    <p v-else-if="error" class="error" role="alert">{{ error }}</p>
    <ul v-else class="users-list">
      <li v-for="user in users" :key="user.id" class="user-card">
        <span>{{ user.firstName }} {{ user.lastName }} {{ user.maidenName }}</span>
        <span class="user-email">{{ user.email }}</span>
      </li>
    </ul>
  </section>
</template>
