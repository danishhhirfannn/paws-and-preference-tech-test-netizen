<script setup>
import MainPage from '@/components/MainPage.vue';
import BottomNavigation from '@/components/BottomNavigation.vue';
</script>

<template>
  <div class="h-screen bg-gradient-to-b from-[var(--p-primary-50)] to-[var(--p-primary-700)] dark:from-gray-900 dark:to-gray-800 flex flex-col overflow-hidden">
    <!-- Main Content Area -->
    <main class="flex-1 overflow-hidden">
      <MainPage />
    </main>
    
    <!-- Bottom Navigation -->
    <BottomNavigation />
  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
