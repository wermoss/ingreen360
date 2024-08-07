<script setup lang="ts">
import { ref, onMounted } from "vue";
import { type Content } from "@prismicio/client";

// The array passed to `getSliceComponentProps` is purely optional.
// Consider it as a visual hint for you when templating your slice.
defineProps(
  getSliceComponentProps<Content.ContentTimelineSlice>([
    "slice",
    "index",
    "slices",
    "context",
  ]),
);

const windowWidth = ref(0);

onMounted(() => {
  windowWidth.value = window.innerWidth;
  window.addEventListener("resize", () => {
    windowWidth.value = window.innerWidth;
  });
});
</script>

<template>
  <section
    :data-slice-type="slice.slice_type"
    :data-slice-variation="slice.variation"
  >
    <div
      class="container mx-auto my-20 flex w-full flex-col justify-center lg:flex-row"
    >
      <div
        class="relative flex flex-col items-start justify-start lg:flex-row lg:items-center"
        v-for="(item, index) in slice.primary.steps"
        :key="index"
      >
        <div class="relative flex flex-row items-center lg:flex-col">
          <div
            class="relative flex h-[100px] w-auto justify-center lg:h-full lg:w-full"
          >
            <div
              v-if="
                (windowWidth >= 1024 && index !== 0) ||
                (windowWidth < 1024 && index < slice.primary.steps.length - 1)
              "
              class="absolute flex items-center justify-center lg:right-[50%] lg:top-[50%]"
            >
              <!-- Kreska -->
              <div
                class="h-[100px] w-[2px] bg-[#18a56b] lg:h-[2px] lg:w-[150px]"
              ></div>
            </div>
            <!-- Kropka -->
            <div
              class="z-10 flex h-[26px] w-[26px] items-center justify-center rounded-full bg-[#18a56b]"
            >
              <span class="text-xs text-white">{{ index + 1 }}</span>
            </div>
          </div>
          <!-- Opis -->
          <div
            class="flex h-[100px] w-[400px] items-start pt-1 text-left text-sm lg:w-[150px] lg:justify-center lg:px-4 lg:pt-3 lg:text-center"
          >
            <p>{{ item.step }}</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
