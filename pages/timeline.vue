<template>
  <section>
    <div class="relative mt-40 flex items-center">
      <!-- Elementy osi czasu -->
      <div
        class="relative flex flex-col items-center"
        v-for="(item, index) in timelineItems"
        :key="index"
      >
        <!-- Kropla -->
        <div
          class="z-10 flex h-8 w-8 items-center justify-center rounded-full bg-blue-500"
        >
          <span class="text-white">{{ index + 1 }}</span>
        </div>
        <!-- Kreska (nie dla ostatniego elementu) -->
        <div
          v-if="index < timelineItems.length - 1"
          class="absolute left-full top-4 h-1 w-16 bg-gray-300"
        ></div>
        <!-- Treść -->
        <div class="mt-4 text-center">
          <h3 class="text-lg font-semibold">{{ item.title }}</h3>
          <p class="mt-2 text-sm text-gray-600">{{ item.description }}</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const timelineItems = [
  { title: "Krok 1", description: "Opis kroku 1" },
  { title: "Krok 2", description: "Opis kroku 2" },
  { title: "Krok 3", description: "Opis kroku 3" },
  { title: "Krok 4", description: "Opis kroku 4" },
];
</script>
