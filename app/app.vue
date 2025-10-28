<script setup>
// Theme definitions
const themes = [
  {
    name: 'ocean',
    label: 'Ocean Breeze',
    bg: 'bg-gradient-to-br from-blue-900 via-blue-800 to-indigo-900',
    title: 'text-white',
    text: 'text-blue-100',
    muted: 'text-blue-300',
    accent: 'bg-blue-400',
    button: 'bg-gradient-to-r from-blue-500 to-indigo-500 focus:ring-blue-400'
  },
  {
    name: 'forest',
    label: 'Forest Calm',
    bg: 'bg-gradient-to-br from-green-900 via-emerald-800 to-teal-900',
    title: 'text-white',
    text: 'text-green-100',
    muted: 'text-green-300',
    accent: 'bg-emerald-400',
    button: 'bg-gradient-to-r from-green-500 to-emerald-500 focus:ring-green-400'
  },
  {
    name: 'sunset',
    label: 'Warm Sunset',
    bg: 'bg-gradient-to-br from-orange-900 via-red-800 to-pink-900',
    title: 'text-white',
    text: 'text-orange-100',
    muted: 'text-orange-300',
    accent: 'bg-orange-400',
    button: 'bg-gradient-to-r from-orange-500 to-pink-500 focus:ring-orange-400'
  },
  {
    name: 'midnight',
    label: 'Midnight Hour',
    bg: 'bg-gradient-to-br from-gray-900 via-slate-800 to-zinc-900',
    title: 'text-white',
    text: 'text-gray-100',
    muted: 'text-gray-400',
    accent: 'bg-gray-400',
    button: 'bg-gradient-to-r from-gray-600 to-slate-600 focus:ring-gray-400'
  },
  {
    name: 'amethyst',
    label: 'Amethyst Dream',
    bg: 'bg-gradient-to-br from-purple-900 via-violet-800 to-fuchsia-900',
    title: 'text-white',
    text: 'text-purple-100',
    muted: 'text-purple-300',
    accent: 'bg-purple-400',
    button: 'bg-gradient-to-r from-purple-500 to-fuchsia-500 focus:ring-purple-400'
  }
]

// Current theme state
const currentTheme = ref(themes[0])

// Theme switching function
const switchTheme = (themeName) => {
  const newTheme = themes.find(theme => theme.name === themeName)
  if (newTheme) {
    currentTheme.value = newTheme
  }
}

// Set page title
useHead({
  title: 'Welcome - Nuxt App'
})
</script>

<template>
  <div 
    class="min-h-screen flex items-center justify-center transition-colors duration-500 ease-in-out relative overflow-hidden"
    :class="currentTheme.bg"
  >
    <!-- Subtle animated background -->
    <div class="absolute inset-0 opacity-5">
      <div class="absolute top-1/4 left-1/4 w-96 h-96 bg-white rounded-full blur-3xl animate-float-slow"></div>
      <div class="absolute bottom-1/3 right-1/3 w-80 h-80 bg-white rounded-full blur-3xl animate-float-slow-delay"></div>
    </div>

    <div class="text-center max-w-2xl mx-auto px-6 relative z-10">
      <!-- Main Welcome Content -->
      <div class="mb-12">
        <h1 
          class="text-6xl md:text-7xl font-bold mb-6 transition-colors duration-500"
          :class="currentTheme.title"
        >
          Welcome
        </h1>
        
        <p 
          class="text-xl md:text-2xl mb-8 leading-relaxed transition-colors duration-500"
          :class="currentTheme.text"
        >
          A minimal space for your next big idea
        </p>
        
        <div 
          class="w-24 h-1 mx-auto mb-8 rounded-full transition-colors duration-500"
          :class="currentTheme.accent"
        ></div>
      </div>

      <!-- Interactive Theme Switcher -->
      <div class="space-y-6">
        <p 
          class="text-sm uppercase tracking-wider font-medium transition-colors duration-500"
          :class="currentTheme.muted"
        >
          Choose your vibe
        </p>
        
        <div class="flex justify-center space-x-4">
          <button
            v-for="theme in themes"
            :key="theme.name"
            @click="switchTheme(theme.name)"
            class="group relative w-16 h-16 rounded-full border-2 transition-all duration-300 hover:scale-110 focus:outline-none focus:ring-4 focus:ring-opacity-50"
            :class="[
              theme.button,
              currentTheme.name === theme.name 
                ? 'border-white shadow-lg scale-105' 
                : 'border-transparent hover:border-white/30'
            ]"
            :title="theme.label"
          >
            <span class="absolute inset-0 rounded-full opacity-0 group-hover:opacity-20 transition-opacity duration-300 bg-white"></span>
            <span class="sr-only">{{ theme.label }}</span>
          </button>
        </div>
        
        <p 
          class="text-sm font-medium transition-colors duration-500"
          :class="currentTheme.text"
        >
          {{ currentTheme.label }}
        </p>
      </div>
      
      <!-- Subtle Footer -->
      <div class="mt-16">
        <p 
          class="text-xs transition-colors duration-500"
          :class="currentTheme.muted"
        >
          Built with Nuxt & Tailwind
        </p>
      </div>
    </div>
  </div>
</template>

<style>
/* Subtle floating animation for background elements */
@keyframes float-slow {
  0%, 100% { 
    transform: translateY(0px) translateX(0px); 
  }
  33% { 
    transform: translateY(-30px) translateX(20px); 
  }
  66% { 
    transform: translateY(20px) translateX(-15px); 
  }
}

@keyframes float-slow-delay {
  0%, 100% { 
    transform: translateY(0px) translateX(0px); 
  }
  33% { 
    transform: translateY(25px) translateX(-20px); 
  }
  66% { 
    transform: translateY(-20px) translateX(15px); 
  }
}

.animate-float-slow {
  animation: float-slow 20s ease-in-out infinite;
}

.animate-float-slow-delay {
  animation: float-slow-delay 25s ease-in-out infinite;
}
</style>