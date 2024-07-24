<script setup lang="ts">
import { type Content } from "@prismicio/client";

const serializer = {
  heading2: ({ children }) =>
    `<h2 class="font-semibold text-lg mb-4 last:mb-0">${children}</h2>`,
  heading3: ({ children }) =>
    `<h3 class="font-semibold text-lg mb-4 last:mb-0">${children}</h3>`,
  paragraph: ({ children }) => `<p class="mb-4 last:mb-0">${children}</p>`,
};

// The array passed to `getSliceComponentProps` is purely optional.
// Consider it as a visual hint for you when templating your slice.
defineProps(
  getSliceComponentProps<Content.ContentASlice>([
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
    <div class="container mx-auto px-6 my-10">
      <PrismicRichText
        :field="slice.primary.content"
        :serializer="serializer"
      />
    </div>
  </section>
</template>
