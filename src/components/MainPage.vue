<template>
    <div class="h-full">
      <!-- Header -->
      <header class="flex-shrink-0">
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
      <main class="flex-1">
        <div class="h-full flex items-center justify-center p-4">
          <div class="relative w-full max-w-[400px] h-[90vh] max-h-[600px]">
            <!-- Loading state -->
            <div v-if="isLoading" class="w-full h-full flex items-center justify-center bg-gray-200 rounded-lg">
              <div class="text-center">
                <div class="animate-spin rounded-full h-12 w-12 border-b-2 border-purple-600 mx-auto mb-4"></div>
                <p class="text-gray-600">Loading cats...</p>
              </div>
            </div>
            
            <!-- Stacked Cat Cards -->
            <div v-else-if="catImages.length > 0 && currentCatIndex < catImages.length" class="relative">
              <!-- Top Card (Swipeable) -->
              <Card 
                class="absolute w-full h-full top-0 left-0"
                :style="`overflow: hidden; background: url('${catImages[currentCatIndex]}') center center; background-size: cover; padding: 0; transform: translate(${dragOffset.x}px, ${dragOffset.y}px) rotate(${dragOffset.x * 0.1}deg); transition: ${isDragging ? 'none' : 'transform 0.3s ease-out'}; cursor: grab; z-index: 300;`"
                @mousedown="handleTouchStart"
                @mousemove="handleTouchMove"
                @mouseup="handleTouchEnd"
                @mouseleave="handleTouchEnd"
                @touchstart="handleTouchStart"
                @touchmove="handleTouchMove"
                @touchend="handleTouchEnd"
              >
                <!-- Like/Dislike overlay indicators -->
                <div v-if="Math.abs(dragOffset.x) > 50" class="absolute inset-0 flex items-center justify-center">
                  <div v-if="dragOffset.x > 0" class="bg-green-500 bg-opacity-80 text-white px-6 py-3 rounded-lg text-2xl font-bold transform rotate-12 border-4 border-white">
                    LIKE ❤️
                  </div>
                  <div v-else class="bg-red-500 bg-opacity-80 text-white px-6 py-3 rounded-lg text-2xl font-bold transform -rotate-12 border-4 border-white">
                    NOPE 💔
                  </div>
                </div>
              </Card>
              
              <!-- Second Card (Tilt Left) -->
              <Card 
                v-if="currentCatIndex + 1 < catImages.length"
                class="absolute w-full h-full top-0 left-0 translate-y-2"
                :style="`overflow: hidden; background: url('${catImages[currentCatIndex + 1]}') center center; background-size: cover; padding: 0; transform: rotate(-1deg); z-index: 200;`"
              ></Card>
              
              <!-- Third Card (Tilt Right) -->
              <Card 
                v-if="currentCatIndex + 2 < catImages.length"
                class="absolute w-full h-full top-0 left-0 translate-y-4"
                :style="`overflow: hidden; background: url('${catImages[currentCatIndex + 2]}') center center; background-size: cover; padding: 0; transform: rotate(1deg); z-index: 200;`"
              ></Card>
            </div>
            
            <!-- Tinder-style action buttons -->
            <div v-if="catImages.length > 0 && currentCatIndex < catImages.length" class="absolute bottom-10 left-1/2 transform -translate-x-1/2 flex items-center space-x-4" style="z-index: 400;">
              <!-- Dislike button -->
              <button 
                @click="dislikeCat" 
                class="bg-white bg-opacity-90 hover:bg-opacity-100 text-red-500 rounded-full p-4 shadow-lg transition-all duration-200 hover:scale-110"
                title="Dislike"
              >
                <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
                </svg>
              </button>
              
              <!-- Like button -->
              <button 
                @click="likeCat" 
                class="bg-white bg-opacity-90 hover:bg-opacity-100 text-green-500 rounded-full p-4 shadow-lg transition-all duration-200 hover:scale-110"
                title="Like"
              >
                <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z" />
                </svg>
              </button>
            </div>
            
            <!-- Stats and refresh button -->
            <div v-if="catImages.length > 0" class="absolute top-4 right-4 flex items-center space-x-2" style="z-index: 400;">
              <!-- Stats -->
              <div class="bg-white bg-opacity-80 text-gray-800 px-3 py-1 rounded-full text-sm font-medium">
                ❤️ {{ likedCats.length }} | 💔 {{ dislikedCats.length }}
              </div>
              
              <!-- Refresh button -->
              <button 
                @click="refreshCats" 
                class="bg-white bg-opacity-80 hover:bg-opacity-100 text-gray-800 rounded-full p-2 shadow-lg transition-all duration-200"
                title="Start over"
              >
                <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15" />
                </svg>
              </button>
            </div>
          </div>
        </div>
      </main>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue'
  import Card from '@/volt/Card.vue';
  
  const mobileMenuOpen = ref(false)
  const catImages = ref([])
  const currentCatIndex = ref(0)
  const isLoading = ref(false)
  const likedCats = ref([])
  const dislikedCats = ref([])
  const isDragging = ref(false)
  const dragOffset = ref({ x: 0, y: 0 })
  const startPos = ref({ x: 0, y: 0 })
  
  const toggleMobileMenu = () => {
    mobileMenuOpen.value = !mobileMenuOpen.value
  }
  
  // Function to get a single random cat image from CATAAS API
  const getRandomCat = async () => {
    try {
      const response = await fetch('https://cataas.com/cat?width=800&height=800')
      if (response.ok) {
        const blob = await response.blob()
        return URL.createObjectURL(blob)
      }
    } catch (error) {
      console.error('Error fetching cat image:', error)
      return 'https://primefaces.org/cdn/primevue/images/card-vue.jpg'
    }
  }
  
  // Function to fetch multiple cats (max 10)
  const fetchMultipleCats = async (count = 10) => {
    isLoading.value = true
    try {
      const promises = []
      for (let i = 0; i < count; i++) {
        promises.push(getRandomCat())
      }
      
      const results = await Promise.all(promises)
      catImages.value = results.filter(url => url) // Filter out any failed requests
      currentCatIndex.value = 0
    } catch (error) {
      console.error('Error fetching multiple cats:', error)
    } finally {
      isLoading.value = false
    }
  }
  
  // Function to like current cat
  const likeCat = () => {
    if (catImages.value.length > 0 && currentCatIndex.value < catImages.value.length) {
      const currentCat = catImages.value[currentCatIndex.value]
      likedCats.value.push(currentCat)
      nextCat()
    }
  }
  
  // Function to dislike current cat
  const dislikeCat = () => {
    if (catImages.value.length > 0 && currentCatIndex.value < catImages.value.length) {
      const currentCat = catImages.value[currentCatIndex.value]
      dislikedCats.value.push(currentCat)
      nextCat()
    }
  }
  
  // Function to navigate to next cat (forward only)
  const nextCat = () => {
    if (catImages.value.length > 0) {
      currentCatIndex.value++
      // If we've seen all cats, fetch more
      if (currentCatIndex.value >= catImages.value.length) {
        fetchMultipleCats(5) // Fetch 5 more cats
      }
    }
  }
  
  // Function to refresh all cats
  const refreshCats = () => {
    fetchMultipleCats(10)
    likedCats.value = []
    dislikedCats.value = []
    currentCatIndex.value = 0
  }
  
  // Touch/Mouse event handlers for swipe gestures
  const handleTouchStart = (e) => {
    isDragging.value = true
    const touch = e.touches ? e.touches[0] : e
    startPos.value = { x: touch.clientX, y: touch.clientY }
    dragOffset.value = { x: 0, y: 0 }
  }
  
  const handleTouchMove = (e) => {
    if (!isDragging.value) return
    e.preventDefault()
    const touch = e.touches ? e.touches[0] : e
    dragOffset.value = {
      x: touch.clientX - startPos.value.x,
      y: touch.clientY - startPos.value.y
    }
  }
  
  const handleTouchEnd = () => {
    if (!isDragging.value) return
    isDragging.value = false
    
    const threshold = 100 // Minimum distance for swipe
    const { x, y } = dragOffset.value
    
    // Only trigger on horizontal swipes (left or right)
    if (Math.abs(x) > threshold && Math.abs(x) > Math.abs(y)) {
      if (x > 0) {
        // Swipe right - like
        likeCat()
      } else {
        // Swipe left - dislike
        dislikeCat()
      }
    }
    
    dragOffset.value = { x: 0, y: 0 }
  }
  
  // Load cats when component mounts
  onMounted(() => {
    fetchMultipleCats(10)
  })
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
  
  /* Ensure cards are fully visible on mobile */
  @media (max-width: 640px) {
    .relative {
      width: 90vw !important;
      max-width: 360px !important;
      height: 70vh !important;
      max-height: 500px !important;
    }
  
    /* Adjust button positioning for smaller screens */
    .absolute.bottom-10 {
      bottom: 5px;
      transform: translateX(-50%) scale(0.8);
    }
  
    /* Adjust stats positioning */
    .absolute.top-4.right-4 {
      top: 2px;
      right: 2px;
      transform: scale(0.8);
    }
  }
  </style>