<script setup lang="ts">
import { type Content } from "@prismicio/client";

// The array passed to `getSliceComponentProps` is purely optional.
// Consider it as a visual hint for you when templating your slice.
defineProps(
  getSliceComponentProps<Content.CoverageDSlice>([
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
      <div
        class="grid lg:bg-white lg:grid-cols-2 lg:p-10 gap-4 my-4 rounded mx-6 text-[13px] lg:text-[16px] tracking-wide"
      >
        <div class="flex items-center">
          <div class="w-2 h-2 bg-[#18A56B] mr-4 lg:hidden"></div>
          <div>{{ slice.primary.coverage }}</div>
        </div>
        <div class="grid grid-cols-2 text-center gap-4">
          <div
            v-for="item in slice.primary.variants"
            :key="item.variant"
            class="bg-white p-[22px] lg:p-10 lg:p-0 rounded flex justify-center items-center"
          >
            <Yes v-if="item.variant" />
            <No v-else />
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
