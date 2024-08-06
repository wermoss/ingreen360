<template>
  <nav aria-label="breadcrumb">
    <ol class="m-0 flex list-none p-0 text-[10px] tracking-[0.2em] md:text-xs">
      <li class="breadcrumb-item flex items-center">
        <NuxtLink to="/" class="uppercase">Home</NuxtLink>
      </li>
      <li
        v-for="(crumb, index) in breadcrumbs"
        :key="index"
        class="breadcrumb-item flex items-center"
      >
        <span class="mx-2">/</span>
        <NuxtLink
          v-if="index < breadcrumbs.length - 1"
          :to="crumb.path"
          class="uppercase"
        >
          {{ crumb.name }}
        </NuxtLink>
        <span v-else class="uppercase text-[#18a56b]">{{ crumb.name }}</span>
      </li>
    </ol>
  </nav>
</template>

<script setup lang="ts">
import { useRoute } from "vue-router";
import { computed } from "vue";

const route = useRoute();

const breadcrumbs = computed(() => {
  const pathArray = route.path.split("/").filter((path) => path);
  return pathArray.map((path, index) => {
    let name = path.charAt(0).toUpperCase() + path.slice(1);
    if (index === pathArray.length - 1) {
      name = name.replace(/-/g, " "); // Replace hyphens with spaces in the last element
    }
    return {
      name: name,
      path: "/" + pathArray.slice(0, index + 1).join("/"),
    };
  });
});
</script>

<style scoped>
/* No custom styles needed as we are using Tailwind CSS */
</style>
