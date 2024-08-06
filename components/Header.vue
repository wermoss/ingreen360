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
        <button
          @click="toggleMenu"
          @keydown.space.prevent="toggleMenu"
          @keydown.enter.prevent="toggleMenu"
          class="hamburger hamburger--elastic z-50"
          :class="{ 'is-active': isMenuVisible }"
          aria-label="Menu"
          :aria-expanded="isMenuVisible"
        >
          <div class="hamburger-box">
            <div class="hamburger-inner"></div>
          </div>
        </button>
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

<style scoped>
.hamburger {
  padding: 15px 15px;
  display: inline-block;
  cursor: pointer;
  transition-property: opacity, filter;
  transition-duration: 0.15s;
  transition-timing-function: linear;
  font: inherit;
  color: inherit;
  text-transform: none;
  background-color: transparent;
  border: 0;
  margin: 0;
  overflow: visible;
}
.hamburger:hover {
  opacity: 0.7;
}
.hamburger.is-active:hover {
  opacity: 0.7;
}
.hamburger.is-active .hamburger-inner,
.hamburger.is-active .hamburger-inner::before,
.hamburger.is-active .hamburger-inner::after {
  background-color: #000;
}

.hamburger-box {
  width: 40px;
  height: 24px;
  display: inline-block;
  position: relative;
}

.hamburger-inner {
  display: block;
  top: 50%;
  margin-top: -2px;
}
.hamburger-inner,
.hamburger-inner::before,
.hamburger-inner::after {
  width: 40px;
  height: 4px;
  background-color: #000;
  border-radius: 4px;
  position: absolute;
  transition-property: transform;
  transition-duration: 0.15s;
  transition-timing-function: ease;
}
.hamburger-inner::before,
.hamburger-inner::after {
  content: "";
  display: block;
}
.hamburger-inner::before {
  top: -10px;
}
.hamburger-inner::after {
  bottom: -10px;
}

/*
   * Elastic
   */
.hamburger--elastic .hamburger-inner {
  top: 2px;
  transition-duration: 0.275s;
  transition-timing-function: cubic-bezier(0.68, -0.55, 0.265, 1.55);
}
.hamburger--elastic .hamburger-inner::before {
  top: 10px;
  transition: opacity 0.125s 0.275s ease;
}
.hamburger--elastic .hamburger-inner::after {
  top: 20px;
  transition: transform 0.275s cubic-bezier(0.68, -0.55, 0.265, 1.55);
}

.hamburger--elastic.is-active .hamburger-inner {
  transform: translate3d(0, 10px, 0) rotate(135deg);
  transition-delay: 0.075s;
}
.hamburger--elastic.is-active .hamburger-inner::before {
  transition-delay: 0s;
  opacity: 0;
}
.hamburger--elastic.is-active .hamburger-inner::after {
  transform: translate3d(0, -20px, 0) rotate(-270deg);
  transition-delay: 0.075s;
}
</style>
