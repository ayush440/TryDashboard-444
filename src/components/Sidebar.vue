<template>
  <div class="sidebar" :class="{ 'sidebar-mobile': isMobileMenuOpen }">
    <div class="logo text-black font-bold">
      <img src=" " alt="" />
      <span>Logo Here </span>
    </div>
    <button @click="toggleMobileMenu" class="mobile-menu-toggle md:hidden">
      <i class="icon-menu"></i>
    </button>
    <nav :class="{ 'hidden': !isMobileMenuOpen, 'md:block': true }">
      <div>
        <router-link 
          v-for="item in menuItems" 
          :key="item.path" 
          :to="item.path" 
          :class="[
            'nav-item',
            'transition-all duration-50 rounded-lg cursor-pointer',
            $route.path === item.path ? 'active bg-[#5847f7] text-white' : 'hover:bg-[#5847f7] hover:text-white'
          ]"
        >
          <i :class="item.icon"></i>
          <span>{{ item.name }}</span>
        </router-link>
      </div>
    </nav>
    <!-- Rest of the sidebar content -->
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()
const showUserMenu = ref(false)
const isMobileMenuOpen = ref(false)

const menuItems = [
  { name: 'Home', path: '/', icon: 'icon-home' },
  { name: 'Strategy', path: '/strategy', icon: 'icon-strategy' },
  { name: 'Broker', path: '/broker', icon: 'icon-broker' },
  { name: 'Orders', path: '/orders', icon: 'icon-orders' },
  { name: 'Positions', path: '/positions', icon: 'icon-positions' },
  { name: 'Tutorials', path: '/tutorials', icon: 'icon-tutorials' },
]

const toggleMobileMenu = () => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value
}

const refreshData = () => {
  // Implement refresh logic
}

const logout = () => {
  // Implement logout logic
}
</script>

<style scoped>
.sidebar {
  width: 250px;
  background-color: white;
  color: white;
  padding: 20px;
  display: flex;
  flex-direction: column;
  height: 100vh;
  position: fixed;
  left: 0;
  top: 0;
  z-index: 1000;
  transition: transform 0.3s ease-in-out;
}

.logo {
  display: flex;
  align-items: center;
  margin-bottom: 30px;
}

.nav-item {
  display: flex;
  align-items: center;
  padding: 10px;
  margin-bottom: 10px;
  text-decoration: none;
  color: grey;
  border-radius: 8px; /* Set a consistent border radius */
  height: 40px; /* Set a fixed height */
}

.nav-item:hover, .nav-item.active {
  color: white;
}


.user-profile {
  margin-top: auto;
  display: flex;
  align-items: center;
}

.avatar {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  margin-right: 10px;
}

.user-menu-dropdown {
  position: absolute;
  background-color: white;
  border-radius: 8px;
  padding: 10px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.mobile-menu-toggle {
  display: none;
}

@media (max-width: 768px) {
  .sidebar {
    transform: translateX(-100%);
  }

  .sidebar-mobile {
    transform: translateX(0);
  }

  .mobile-menu-toggle {
    display: block;
    position: absolute;
    top: 20px;
    right: -40px;
    background-color: #5847f7;
    color: white;
    border: none;
    padding: 10px;
    border-radius: 0 5px 5px 0;
  }
}
</style>