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
      <Broadcrumb />

      <h1 class="mb-6 mt-6 text-3xl">{{ slice.primary.text }}</h1>

      <!-- 
      <h1
        class="mb-10 inline-block rounded-md bg-[#18a56b] px-6 py-2 text-xl tracking-widest text-white"
      >
        {{ slice.primary.text }}
      </h1> -->
      <p class="mb-14">
        Pakiet zapewniający natychmiastową pomoc w nagłej sytuacji. W ramach
        świadczenia otrzymasz holowanie pojazdu, dowóz paliwa, pojazd zastępczy,
        zakwaterowanie i wiele innyh elementów
      </p>
    </div>
  </section>
</template>
