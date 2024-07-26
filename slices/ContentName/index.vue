<script setup lang="ts">
import { type Content } from "@prismicio/client";

// The array passed to `getSliceComponentProps` is purely optional.
// Consider it as a visual hint for you when templating your slice.
defineProps(
  getSliceComponentProps<Content.ContentNameSlice>([
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
    <div class="container mx-auto px-6">
      <h1
        class="mb-10 inline-block rounded-md bg-[#18a56b] px-6 py-2 text-xl tracking-widest text-white"
      >
        {{ slice.primary.text }}
      </h1>
    </div>
  </section>
</template>
