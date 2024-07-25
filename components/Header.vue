<script setup lang="ts">
import { ref, watch, onMounted } from "vue";
import { useRoute } from "vue-router";
import { gsap } from "gsap";
import MenuComponent from "./MenuComponent.vue"; // Dodaj ten import

const route = useRoute();
const prismic = usePrismic();
const { data: aaa } = useAsyncData("aaa", () =>
  prismic.client.getSingle("header"),
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
  <section class="absolute w-full bg-white py-6">
    <div class="container mx-auto flex items-center justify-between px-6">
      <NuxtLink to="/" class="text-[#18a56b]"
        ><img src="/img/logo.svg" class="w-[150px] lg:w-[200px]"
      /></NuxtLink>
      <div class="flex flex-row items-center gap-8">
        <div @click="toggleMenu" class="z-50">Menu</div>
        <div
          class="rounded-md bg-[#18a56b] px-4 py-2 text-xs tracking-widest text-white lg:text-sm"
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
