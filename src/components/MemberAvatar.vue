<script setup lang="ts">
defineProps<{
  name: string
  avatar: string
  isHost?: boolean
  isGuest?: boolean
  size?: 'sm' | 'md' | 'lg'
}>()
</script>

<template>
  <div 
    class="member-avatar flex flex-col items-center gap-1"
    :class="{
      'w-12': size === 'sm',
      'w-16': size === 'md' || !size,
      'w-24': size === 'lg'
    }"
  >
    <div 
      class="avatar-circle relative rounded-full flex items-center justify-center bg-gradient-to-br from-white to-gray-100 shadow-md border-2 border-white"
      :class="{
        'w-10 h-10 text-xl': size === 'sm',
        'w-14 h-14 text-2xl': size === 'md' || !size,
        'w-20 h-20 text-4xl': size === 'lg',
        'ring-2 ring-yellow-400 ring-offset-2': isHost,
        'ring-2 ring-cyan-400 ring-offset-2': isGuest && !isHost
      }"
    >
      <span class="transform hover:scale-110 transition-transform">{{ avatar }}</span>
      <span 
        v-if="isHost" 
        class="absolute -top-1 -right-1 text-xs bg-yellow-400 rounded-full px-1 py-0.5"
      >
        👑
      </span>
      <span 
        v-if="isGuest && !isHost" 
        class="absolute -top-1 -right-1 text-xs bg-cyan-400 rounded-full px-1 py-0.5"
      >
        ⭐
      </span>
    </div>
    <div class="flex items-center gap-1">
      <span 
        class="text-center font-medium truncate"
        :class="{
          'text-xs': size === 'sm',
          'text-sm': size === 'md' || !size,
          'text-base': size === 'lg'
        }"
      >
        {{ name }}
      </span>
      <span 
        v-if="isGuest && !isHost"
        class="text-[10px] bg-cyan-100 text-cyan-700 px-1.5 py-0.5 rounded-full font-medium whitespace-nowrap"
      >
        嘉宾
      </span>
    </div>
  </div>
</template>
