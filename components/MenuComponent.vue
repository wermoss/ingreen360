<template>
  <div
    class="menu-animation fixed left-0 top-0 z-10 h-screen w-[450px] bg-white px-10 pt-6 shadow-xl"
  >
    <img src="/img/logo.svg" class="pb-10" />
    <div
      v-for="item in menuItems"
      :key="item.link.id"
      class="tracking-wides pl-8 text-[16px] font-normal"
    >
      <PrismicLink :field="item.link" @click="toggleMenu">
        <p class="py-1">{{ item.label }}</p>
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
