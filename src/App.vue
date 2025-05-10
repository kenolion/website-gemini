<template>
  <div class="flex flex-col min-h-screen">
    <header class="bg-green-600 text-white p-4 shadow-md sticky top-0 z-30">
      <div class="container mx-auto flex items-center">
        <button
          @click="toggleSidebar"
          class="p-2 rounded-md hover:bg-green-700 focus:outline-none focus:ring-2 focus:ring-white mr-4"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="currentColor"
            class="w-6 h-6"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25h16.5"
            />
          </svg>
        </button>
        <h1 class="text-xl font-semibold">Vue PWA with Vite</h1>
      </div>
    </header>

    <div
      v-if="isSidebarOpen"
      @click="closeSidebar"
      class="fixed inset-0 bg-black bg-opacity-50 z-40 overlay"
    ></div>

    <aside
      :class="[
        'fixed top-0 left-0 w-64 h-full bg-gray-800 text-white p-5 z-50 sidebar-transition rounded-r-lg shadow-xl',
        isSidebarOpen ? 'sidebar-open' : 'sidebar-closed',
      ]"
    >
      <div class="flex justify-between items-center mb-6">
        <h2 class="text-2xl font-bold">Menu</h2>
        <button
          @click="closeSidebar"
          class="p-1 rounded-md hover:bg-gray-700 focus:outline-none focus:ring-2 focus:ring-white"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="currentColor"
            class="w-6 h-6"
          >
            <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
          </svg>
        </button>
      </div>
      <nav>
        <ul>
          <li class="mb-3">
            <router-link
              to="/"
              @click="closeSidebar"
              :class="[
                'block py-2 px-3 rounded-md hover:bg-gray-700 transition-colors',
                $route.name === 'Home' ? 'bg-green-500 font-semibold' : '',
              ]"
            >
              Home
            </router-link>
          </li>
          <li class="mb-3">
            <router-link
              to="/about"
              @click="closeSidebar"
              :class="[
                'block py-2 px-3 rounded-md hover:bg-gray-700 transition-colors',
                $route.name === 'About' ? 'bg-green-500 font-semibold' : '',
              ]"
            >
              About
            </router-link>
          </li>
        </ul>
      </nav>
    </aside>

    <main class="flex-grow container mx-auto mt-2 p-4">
      <router-view />
    </main>

    <footer class="bg-gray-200 text-center p-4 mt-auto text-gray-600 rounded-t-lg">
      <p>&copy; {{ new Date().getFullYear() }} Vue PWA Demo</p>
    </footer>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
// import { useRoute, useRouter } from 'vue-router'

const isSidebarOpen = ref(false)
// const route = useRoute() // To get current route for active link styling
// const router = useRouter() // To navigate programmatically if needed, though router-link handles most cases

const toggleSidebar = () => {
  isSidebarOpen.value = !isSidebarOpen.value
}

const closeSidebar = () => {
  isSidebarOpen.value = false
}

// Note: For programmatic navigation within setup, you'd use router.push().
// Here, router-link's @click="closeSidebar" is sufficient.
</script>

<style scoped>
/* Basic transition for sidebar */
.sidebar-transition {
  transition: transform 0.3s ease-in-out;
}
.sidebar-open {
  transform: translateX(0);
}
.sidebar-closed {
  transform: translateX(-100%);
}
/* Overlay for when sidebar is open */
.overlay {
  transition: opacity 0.3s ease-in-out;
}
/* Additional scoped styles can go here */
</style>
