<script setup lang="ts">
import { ref, watch, onMounted } from "vue";
import { useRoute } from "vue-router";
import { gsap } from "gsap";
import MenuComponent from "./MenuComponent.vue"; // Dodaj ten import

const route = useRoute();
const prismic = usePrismic();
const { data: aaa } = useAsyncData("aaa", () =>
  prismic.client.getSingle("header")
);
const isMenuVisible = ref(false);

function toggleMenu() {
  isMenuVisible.value = !isMenuVisible.value;
}

watch(isMenuVisible, (newVal) => {
  if (newVal) {
    gsap.to(".menu-animation", { x: "0%", duration: 0.3 });
  } else {
    gsap.to(".menu-animation", { x: "-100%", duration: 0.3 });
  }
});

onMounted(() => {
  gsap.to(".menu-animation", { x: "-100%", duration: 0.3 });
});
</script>

<template>
  <section class="py-6 absolute w-full bg-white">
    <div class="container mx-auto flex justify-between items-center">
      <NuxtLink to="/" class="text-[#18a56b]">Ubezpiecz Moją Teslę</NuxtLink>
      <div class="flex flex-row gap-8 items-center">
        <div @click="toggleMenu" class="z-50">Menu</div>
        <div
          class="bg-[#18a56b] px-4 py-2 rounded-md text-white border border-white"
        >
          KONTAKT
        </div>
      </div>
    </div>
  </section>

  <!-- Użyj MenuComponent i przekaż odpowiednie propsy -->
  <MenuComponent
    :menuItems="aaa?.data.links"
    :toggleMenu="toggleMenu"
    :currentPath="route.path"
  />
</template>
