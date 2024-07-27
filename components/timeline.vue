<template>
  <section>
    <div class="relative flex flex-col items-start justify-between lg:flex-row">
      <!-- Elementy osi czasu -->
      <div
        class="relative flex h-[100px] w-full flex-col items-center lg:w-[200px] lg:flex-col lg:items-start"
        v-for="(item, index) in timelineItems"
        :key="index"
      >
        <div class="flex w-full items-center lg:flex-col">
          <!-- Kropla -->
          <div
            class="z-10 flex h-8 w-8 items-center justify-center rounded-full bg-[#18a56b]"
          >
            <span class="text-white">{{ index + 1 }}</span>
          </div>
          <!-- Treść -->
          <div
            class="ml-4 w-[200px] text-left text-sm lg:ml-0 lg:mt-4 lg:text-center"
          >
            <!-- <h3 class="text-lg font-semibold">{{ item.title }}</h3> -->
            <p class="text-md mt-2 text-gray-600">{{ item.description }}</p>
          </div>
        </div>
        <!-- Kreska (nie dla ostatniego elementu) -->
        <div
          v-if="index < timelineItems.length - 1"
          class="h-[100px] w-[2px] bg-gray-300 lg:h-[2px] lg:w-[200px]"
          :class="{ 'absolute left-[15px] top-4 lg:left-[100px]': true }"
        ></div>
      </div>
    </div>
  </section>
</template>

<script setup>
const timelineItems = [
  { title: "Krok 1", description: "Problem prawny" },
  { title: "Krok 2", description: "Konsultacja telefoniczna z prawnikiem" },
  {
    title: "Krok 3",
    description: "Udostępnienie dokumentów / aktów prawnych / adresów placówek",
  },
  { title: "Krok 4", description: "Reprezentacja i prowadzenie sprawy" },
  { title: "Krok 5", description: "Zamkniecie sprawy" },
];
</script>
