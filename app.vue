<template>
  <div>
    <!-- Navigation bar visible on all pages except /login and /register -->
    <nav v-if="showNav" class="navbar">
      <NuxtLink to="/">Home</NuxtLink>
      <!-- ADMIN -->
      <NuxtLink v-if="user?.role === 'admin'" to="/manage-menu">Manage Menu</NuxtLink>
      <!-- <NuxtLink v-if="user?.role === 'admin'" to="/manage-services">Manage Services</NuxtLink> -->
      <NuxtLink v-if="user?.role === 'admin'" to="/manage-bookings">Manage Bookings</NuxtLink>
      <NuxtLink v-if="user?.role === 'admin'" to="/admin">Admin</NuxtLink>
      <!-- CUSTOMER -->
      <NuxtLink v-if="user?.role === 'customer'" to="/profile" >My Profile</NuxtLink>
      <NuxtLink  v-if="user?.role === 'customer'" to="/menu-info">Menu</NuxtLink>
      <NuxtLink  v-if="user?.role === 'customer'" to="/services-info">Services</NuxtLink>
      <NuxtLink  v-if="user?.role === 'customer'" to="/gallery-info">Gallery</NuxtLink>
      <button v-if="user" @click="logout">Logout</button>
    </nav>

    <NuxtLayout>
      <NuxtPage />
    </NuxtLayout>
  </div>
</template>

<script setup>
import { useRoute } from 'vue-router'
const { user, logout, initAuth } = useAuth()
initAuth()

const route = useRoute()
const showNav = computed(() => !['/login', '/register'].includes(route.path))
</script>

<style scoped>
.navbar {
  position: sticky;
  top: 0;
  background: white;
  padding: 1rem;
  display: flex;
  gap: 1rem;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  z-index: 1000;
}
</style>
