<template>
  <div class="min-h-screen bg-gradient-to-b from-[var(--p-primary-50)] to-[var(--p-primary-700)] dark:from-gray-900 dark:to-gray-800">
    <!-- Header -->
    <header>
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex justify-between items-center h-16">
          <!-- Logo/Brand -->
          <div class="flex items-center">
            <h1 class="text-xl font-bold text-gray-900 dark:text-white">
              Paws & Preference
            </h1>
          </div>
          
          <!-- Mobile menu button -->
          <div class="md:hidden">
            <button 
              @click="toggleMobileMenu"
              class="text-gray-500 hover:text-gray-700 dark:text-gray-400 dark:hover:text-gray-200"
            >
              <svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
              </svg>
            </button>
          </div>
          
          <!-- Desktop Navigation -->
          <nav class="hidden md:flex space-x-8">
            <a href="#" class="text-gray-700 hover:text-purple-600 dark:text-gray-300 dark:hover:text-purple-400 px-3 py-2 text-sm font-medium">Home</a>
            <a href="#" class="text-gray-700 hover:text-purple-600 dark:text-gray-300 dark:hover:text-purple-400 px-3 py-2 text-sm font-medium">About</a>
            <a href="#" class="text-gray-700 hover:text-purple-600 dark:text-gray-300 dark:hover:text-purple-400 px-3 py-2 text-sm font-medium">Contact</a>
          </nav>
        </div>
        
        <!-- Mobile Navigation -->
        <div v-if="mobileMenuOpen" class="md:hidden">
          <div class="px-2 pt-2 pb-3 space-y-1 sm:px-3 border-t border-gray-200 dark:border-gray-700">
            <a href="#" class="text-gray-700 hover:text-purple-600 dark:text-gray-300 dark:hover:text-purple-400 block px-3 py-2 text-base font-medium">Home</a>
            <a href="#" class="text-gray-700 hover:text-purple-600 dark:text-gray-300 dark:hover:text-purple-400 block px-3 py-2 text-base font-medium">About</a>
            <a href="#" class="text-gray-700 hover:text-purple-600 dark:text-gray-300 dark:hover:text-purple-400 block px-3 py-2 text-base font-medium">Contact</a>
          </div>
        </div>
      </div>
    </header>

    <!-- Main Content -->
    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
      <!-- Hero Section -->
      <section class="text-center mb-12">
        <h2 class="text-3xl sm:text-4xl lg:text-5xl font-bold text-gray-900 dark:text-white mb-4">
          Welcome to <span class="text-purple-600 dark:text-purple-400">Paws & Preference</span>
        </h2>
        <p class="text-lg sm:text-xl text-gray-600 dark:text-gray-300 max-w-3xl mx-auto">
          Discover the perfect companion for your lifestyle. Find your ideal pet match with our intelligent matching system.
        </p>
      </section>

      <!-- Features Grid -->
      <section class="mb-12">
        <h3 class="text-2xl font-bold text-gray-900 dark:text-white mb-8 text-center">
          Why Choose Us?
        </h3>
        
        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
          <!-- Feature Card 1 -->
          <div class="bg-white dark:bg-gray-800 rounded-lg shadow-md p-6 hover:shadow-lg transition-shadow">
            <div class="w-12 h-12 bg-purple-100 dark:bg-purple-900 rounded-lg flex items-center justify-center mb-4">
              <svg class="w-6 h-6 text-purple-600 dark:text-purple-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9.663 17h4.673M12 3v1m6.364 1.636l-.707.707M21 12h-1M4 12H3m3.343-5.657l-.707-.707m2.828 9.9a5 5 0 117.072 0l-.548.547A3.374 3.374 0 0014 18.469V19a2 2 0 11-4 0v-.531c0-.895-.356-1.754-.988-2.386l-.548-.547z" />
              </svg>
            </div>
            <h4 class="text-lg font-semibold text-gray-900 dark:text-white mb-2">Smart Matching</h4>
            <p class="text-gray-600 dark:text-gray-300">Our AI-powered system matches you with pets based on your lifestyle and preferences.</p>
          </div>

          <!-- Feature Card 2 -->
          <div class="bg-white dark:bg-gray-800 rounded-lg shadow-md p-6 hover:shadow-lg transition-shadow">
            <div class="w-12 h-12 bg-blue-100 dark:bg-blue-900 rounded-lg flex items-center justify-center mb-4">
              <svg class="w-6 h-6 text-blue-600 dark:text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z" />
              </svg>
            </div>
            <h4 class="text-lg font-semibold text-gray-900 dark:text-white mb-2">Verified Shelters</h4>
            <p class="text-gray-600 dark:text-gray-300">We partner with verified shelters and rescue organizations to ensure quality care.</p>
          </div>

          <!-- Feature Card 3 -->
          <div class="bg-white dark:bg-gray-800 rounded-lg shadow-md p-6 hover:shadow-lg transition-shadow">
            <div class="w-12 h-12 bg-green-100 dark:bg-green-900 rounded-lg flex items-center justify-center mb-4">
              <svg class="w-6 h-6 text-green-600 dark:text-green-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" />
              </svg>
            </div>
            <h4 class="text-lg font-semibold text-gray-900 dark:text-white mb-2">24/7 Support</h4>
            <p class="text-gray-600 dark:text-gray-300">Get help anytime with our round-the-clock support team and community.</p>
          </div>
        </div>
      </section>

      <!-- CTA Section -->
      <section class="bg-gradient-to-r from-purple-600 to-blue-600 rounded-xl p-8 text-center">
        <h3 class="text-2xl sm:text-3xl font-bold text-white mb-4">
          Ready to Find Your Perfect Match?
        </h3>
        <p class="text-purple-100 mb-6 max-w-2xl mx-auto">
          Join thousands of happy pet parents who found their ideal companion through our platform.
        </p>
        <button class="bg-white text-purple-600 px-8 py-3 rounded-lg font-semibold hover:bg-gray-100 transition-colors">
          Get Started Today
        </button>
      </section>
    </main>

    <!-- Footer -->
    <footer class="bg-gray-900 text-white mt-16">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12">
        <div class="grid grid-cols-1 md:grid-cols-4 gap-8">
          <div class="col-span-1 md:col-span-2">
            <h4 class="text-lg font-semibold mb-4">Paws & Preference</h4>
            <p class="text-gray-400 mb-4">
              Connecting loving homes with wonderful pets. Making adoption simple, safe, and successful.
            </p>
          </div>
          <div>
            <h5 class="font-semibold mb-4">Quick Links</h5>
            <ul class="space-y-2 text-gray-400">
              <li><a href="#" class="hover:text-white">About Us</a></li>
              <li><a href="#" class="hover:text-white">How It Works</a></li>
              <li><a href="#" class="hover:text-white">Success Stories</a></li>
            </ul>
          </div>
          <div>
            <h5 class="font-semibold mb-4">Contact</h5>
            <ul class="space-y-2 text-gray-400">
              <li>support@pawsandpreference.com</li>
              <li>1-800-PAWS-123</li>
            </ul>
          </div>
        </div>
        <div class="border-t border-gray-800 mt-8 pt-8 text-center text-gray-400">
          <p>&copy; 2024 Paws & Preference. All rights reserved.</p>
        </div>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const mobileMenuOpen = ref(false)

const toggleMobileMenu = () => {
  mobileMenuOpen.value = !mobileMenuOpen.value
}
</script>

<style scoped>
/* Custom scrollbar for webkit browsers */
::-webkit-scrollbar {
  width: 8px;
}

::-webkit-scrollbar-track {
  background: #f1f1f1;
}

::-webkit-scrollbar-thumb {
  background: #c1c1c1;
  border-radius: 4px;
}

::-webkit-scrollbar-thumb:hover {
  background: #a8a8a8;
}

/* Dark mode scrollbar */
@media (prefers-color-scheme: dark) {
  ::-webkit-scrollbar-track {
    background: #374151;
  }
  
  ::-webkit-scrollbar-thumb {
    background: #6b7280;
  }
  
  ::-webkit-scrollbar-thumb:hover {
    background: #9ca3af;
  }
}
</style>