<template>
  <footer class="flex-shrink-0 text-white">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
             <div class="flex justify-center items-center h-16">
         <div class="flex items-center space-x-16">
          <a 
            href="#" 
            class="text-gray-300 hover:text-white px-3 py-2 text-sm font-medium flex flex-col items-center transition-colors"
          >
            <svg class="w-5 h-5 mb-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6" />
            </svg>
            <span class="text-xs">Home</span>
          </a>
          <a 
            href="#" 
            class="text-gray-300 hover:text-white px-3 py-2 text-sm font-medium flex flex-col items-center transition-colors"
          >
            <svg class="w-5 h-5 mb-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
            </svg>
            <span class="text-xs">Search</span>
          </a>
          <a 
            href="#" 
            class="text-gray-300 hover:text-white px-3 py-2 text-sm font-medium flex flex-col items-center transition-colors"
          >
            <svg class="w-5 h-5 mb-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" />
            </svg>
            <span class="text-xs">Profile</span>
          </a>
        </div>
      </div>
    </div>
  </footer>
</template>

<script setup>
// Simple bottom navigation component - no active state management
</script>

<style scoped>
/* Mobile optimizations */
@media (max-width: 640px) {
  .space-x-8 > * + * {
    margin-left: 1rem;
  }
}

/* Touch-friendly targets */
a, button {
  min-height: 44px;
  min-width: 44px;
}

/* Smooth transitions */
.transition-colors {
  transition: color 0.2s ease-in-out;
}
</style>
