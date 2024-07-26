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
  >
    {{ slice.primary.title }}
    <div class="grid md:grid-cols-3">
      <div v-for="item in slice.primary.reviews">
        <PrismicImage :field="item.image" />
        {{ item.description }}
      </div>
    </div>
  </section>
</template>
