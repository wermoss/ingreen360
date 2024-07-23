<script setup lang="ts">
import { type Content } from "@prismicio/client";

// The array passed to `getSliceComponentProps` is purely optional.
// Consider it as a visual hint for you when templating your slice.
defineProps(
  getSliceComponentProps<Content.CoverageCSlice>([
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
        class="grid lg:bg-white lg:grid-cols-2 lg:p-10 gap-4 my-2 rounded mx-6 text-[13px] lg:text-[16px] tracking-wide"
      >
        <div>
          {{ slice.primary.coverage }}
        </div>
        <div class="grid grid-cols-2 text-center gap-4">
          <div
            v-for="item in slice.primary.variants"
            class="bg-white p-10 lg:p-0 rounded"
          >
            <p>{{ item.variant }}</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
