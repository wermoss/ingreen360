<template>
  <div class="w-[500px] bg-gray-200 fixed left-0 top-0 h-screen menu-animation">
    <div
      v-for="item in menuItems"
      :key="item.link.id"
      class="text-lg font-normal pl-8 tracking-widest"
    >
      <a
        v-if="item.link.link_type === 'Web'"
        :href="item.link.url"
        target="_blank"
        rel="noopener noreferrer"
        @click="toggleMenu"
        :class="{ 'text-green-500': item.link.url === currentPath }"
      >
        {{ item.label }}
      </a>
      <RouterLink
        v-else
        :to="`/pakiet/${item.link.uid}`"
        @click="toggleMenu"
        :class="{
          'text-green-500': `/pakiet/${item.link.uid}` === currentPath,
        }"
      >
        {{ item.label }}
      </RouterLink>
    </div>
  </div>
</template>

<script setup>
import { defineProps } from "vue";

const props = defineProps({
  menuItems: Array,
  toggleMenu: Function,
  currentPath: String,
});
</script>

<style scoped>
.menu-animation {
  transform: translateX(-100%);
}
</style>
