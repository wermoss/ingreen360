<script setup lang="ts">
import { type Content } from "@prismicio/client";

// The array passed to `getSliceComponentProps` is purely optional.
// Consider it as a visual hint for you when templating your slice.
defineProps(
  getSliceComponentProps<Content.CoverageBSlice>([
    "slice",
    "index",
    "slices",
    "context",
  ])
);
</script>

<template>
  <section
    :data-slice-type="slice.slice_type"
    :data-slice-variation="slice.variation"
  >
    <div class="container mx-auto max-w-8xl">
      <div class="grid lg:grid-cols-2 px-10 gap-4 my-4 rounded mx-6">
        <div class="hidden lg:block">
          <!-- Empty content -->
        </div>
        <div class="grid grid-cols-2 text-center gap-4">
          <div
            v-for="item in slice.primary.packages"
            class="bg-[#16A56B] py-6 rounded-md text-white"
          >
            <p class="text-xs">{{ item.type }}</p>
            <p class="font-semibold">{{ item.name }}</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
