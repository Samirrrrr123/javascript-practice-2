<script>
export default {
  data() {
    return { username: '', password: '', error: '', loading: false }
  },
  methods: {
    async login() {
      this.error = ''
      this.loading = true
      try {
        const response = await fetch('https://dummyjson.com/auth/login', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify({ username: this.username, password: this.password }),
        })
        const data = await response.json()
        if (!response.ok) {
          throw new Error(data.message || 'Authorization failed')
        }
        localStorage.setItem('token', data.accessToken)
        this.$router.push('/profile')
      } catch (error) {
        this.error = error.message
      } finally {
        this.loading = false
      }
    },
  },
}
</script>

<template>
  <section class="login-page">
    <form class="login-card" @submit.prevent="login">
      <div class="form-heading">
        <h1>Authorization</h1>
        <p v-if="error" class="error" role="alert">{{ error }}</p>
      </div>
      <div class="form-fields">
        <label for="username">Login</label>
        <input id="username" v-model="username" name="username" autocomplete="username" required />
        <label for="password">Password</label>
        <input id="password" v-model="password" name="password" type="password" autocomplete="current-password" required />
        <button type="submit" :disabled="loading">{{ loading ? 'Loading...' : 'Submit' }}</button>
      </div>
    </form>
  </section>
</template>
