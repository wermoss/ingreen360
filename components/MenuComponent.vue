<template>
  <div
    class="w-[450px] bg-white fixed left-0 top-0 h-screen p-10 menu-animation shadow-xl"
  >
    <div
      v-for="item in menuItems"
      :key="item.link.id"
      class="text-lg font-normal pl-8 tracking-wides text-[16px]"
    >
      <PrismicLink :field="item.link" @click="toggleMenu">
        {{ item.label }}
      </PrismicLink>
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
