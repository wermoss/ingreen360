<script setup lang="ts">
import { type Content } from "@prismicio/client";

// The array passed to `getSliceComponentProps` is purely optional.
// Consider it as a visual hint for you when templating your slice.
defineProps(
  getSliceComponentProps<Content.ReviewsSlice>([
    "slice",
    "index",
    "slices",
    "context",
  ]),
);
</script>

<template>
  <section
    :data-slice-type="slice.slice_type"
    :data-slice-variation="slice.variation"
    class="mb-10"
  >
    <!-- {{ slice.primary.title }} -->
    <div
      class="grid items-center justify-center gap-10 text-center md:grid-cols-3"
    >
      <div
        v-for="item in slice.primary.reviews"
        class="flex flex-col items-center"
      >
        <PrismicImage :field="item.image" class="mb-10 h-[50px] lg:h-[80px]" />
        <p class="lg:text-md px-20 text-sm lg:px-0">{{ item.description }}</p>
      </div>
    </div>
  </section>
</template>
