<script setup lang="ts">
import { ref, watch, onMounted } from "vue";
import { useRoute } from "vue-router";

import { gsap } from "gsap";
const route = useRoute();

const prismic = usePrismic();
const { data: aaa } = useAsyncData("aaa", () =>
  prismic.client.getSingle("header")
);
const isMenuVisible = ref(false);

function toggleMenu() {
  isMenuVisible.value = !isMenuVisible.value;
}

// Animacja GSAP
watch(isMenuVisible, (newVal) => {
  if (newVal) {
    gsap.to(".menu-animation", { x: "0%", duration: 0.3 });
  } else {
    gsap.to(".menu-animation", { x: "-100%", duration: 0.3 });
  }
});

onMounted(() => {
  // Ustawienie początkowego stanu animacji z określeniem jednostki
  gsap.to(".menu-animation", { x: "-100%", duration: 0.3 });
});
</script>

<template>
  <section class="py-6 absolute w-full bg-white">
    <div class="container mx-auto flex justify-between items-center">
      <NuxtLink to="/" class="text-[#18a56b]">Ubezpiecz Moją Teslę</NuxtLink>
      <div class="flex flex-row gap-8 items-center">
        <div @click="toggleMenu">Menu</div>
        <div
          class="bg-[#18a56b] px-4 py-2 rounded-md text-white border border-white"
        >
          KONTAKT
        </div>
      </div>
    </div>
  </section>

  <div class="w-[500px] bg-gray-200 fixed left-0 top-0 h-screen menu-animation">
    <div
      v-for="item in aaa?.data.links"
      :key="item.link.id"
      class="text-lg font-normal pl-8 tracking-widest"
    >
      <!-- Obsługa linków wewnętrznych i zewnętrznych z dynamicznym przypisaniem klas -->
      <a
        v-if="item.link.link_type === 'Web'"
        :href="item.link.url"
        target="_blank"
        rel="noopener noreferrer"
        @click="toggleMenu"
        :class="{ 'text-green-500': item.link.url === route.path }"
      >
        {{ item.label }}
      </a>
      <RouterLink
        v-else
        :to="`/pakiet/${item.link.uid}`"
        @click="toggleMenu"
        :class="{ 'text-green-500': `/pakiet/${item.link.uid}` === route.path }"
      >
        {{ item.label }}
      </RouterLink>
    </div>
  </div>
</template>

<style scoped>
.menu-animation {
  transform: translateX(-100%);
}
</style>
