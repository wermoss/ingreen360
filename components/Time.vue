<template>
  <section>
    <div
      class="container mx-auto flex w-screen flex-col justify-center bg-green-100 lg:flex-row"
    >
      <div
        class="relative flex flex-col items-start justify-start bg-pink-100 lg:flex-row lg:items-center"
        v-for="(item, index) in timelineItems"
        :key="index"
      >
        <div class="relative flex flex-row items-center lg:flex-col">
          <div
            class="relative flex h-[100px] w-full justify-center bg-yellow-100 lg:h-full"
          >
            <div
              v-if="
                (windowWidth >= 1024 && index !== 0) ||
                (windowWidth < 1024 && index < timelineItems.length - 1)
              "
              class="absolute flex items-center justify-center lg:right-[50%] lg:top-[50%]"
            >
              <!-- Kreska -->
              <div
                class="h-[100px] w-[2px] bg-pink-500 lg:h-[2px] lg:w-[150px]"
              ></div>
            </div>
            <!-- Kropka -->
            <div
              class="z-10 flex h-[30px] w-[30px] items-center justify-center rounded-full bg-[#18a56b]"
            >
              <span class="text-white">{{ index + 1 }}</span>
            </div>
          </div>
          <!-- Opis -->
          <div
            class="flex h-[100px] w-[200px] items-start text-left lg:w-[150px] lg:justify-center lg:px-4 lg:text-center"
          >
            <p>{{ item.description }}</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from "vue";

const timelineItems = [
  {
    title: "Krok 1",
    description: "Opis kroku 1 fsd fsdf sdf sdfs dfsd f sdf sd",
  },
  { title: "Krok 2", description: "Opis kroku 2 fsdf sdf sd fsd f" },
  {
    title: "Krok 3",
    description: "Opis kroku 3 fsdfsdfsd fs dfsd fsd f dsf sdfsd fsd fs",
  },
];

const windowWidth = ref(0);

onMounted(() => {
  windowWidth.value = window.innerWidth;
  window.addEventListener("resize", () => {
    windowWidth.value = window.innerWidth;
  });
});
</script>
