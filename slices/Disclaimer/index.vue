<script setup lang="ts">
import { type Content } from "@prismicio/client";

// The array passed to `getSliceComponentProps` is purely optional.
// Consider it as a visual hint for you when templating your slice.
defineProps(
  getSliceComponentProps<Content.DisclaimerSlice>([
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
  >
    <div class="container mx-auto flex flex-col items-center justify-center">
      <p class="mb-4 text-3xl">{{ slice.primary.title }}</p>
      <PrismicRichText
        :field="slice.primary.disclaimer"
        class="text-md leading-7 text-gray-500"
      />
    </div>
  </section>
</template>
