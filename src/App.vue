<script>
import AppFooter from './components/AppFooter.vue'

export default {
  components: { AppFooter },
}
</script>

<template>
  <header class="header">
    <nav aria-label="Main navigation">
      <RouterLink to="/home">Home</RouterLink>
      <RouterLink to="/users">Users</RouterLink>
      <RouterLink to="/profile">Profile</RouterLink>
    </nav>
  </header>
  <main>
    <RouterView />
  </main>
  <AppFooter />
</template>
