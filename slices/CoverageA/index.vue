<script setup lang="ts">
import { type Content } from "@prismicio/client";

const serializer = {
  heading2: ({ children }) =>
    `<h2 class="font-semibold text-lg mb-4 last:mb-0">${children}</h2>`,
  paragraph: ({ children }) => `<p class="mb-4 last:mb-0">${children}</p>`,
  oList: ({ children }) =>
    /* html */ `<ol class="mb-7 pl-4 last:mb-0 md:pl-6">${children}</ol>`,
  oListItem: ({ children }) =>
    /* html */ `<li class="mb-1 list-decimal pl-1 last:mb-0 md:pl-2">${children}</li>`,
  list: ({ children }) =>
    /* html */ `<ul class="mb-7 pl-4 last:mb-0 md:pl-6">${children}</ul>`,
  listItem: ({ children }) =>
    /* html */ `<li class="mb-1 list-disc pl-1 last:mb-0 md:pl-2">${children}</li>`,
};

// The array passed to `getSliceComponentProps` is purely optional.
// Consider it as a visual hint for you when templating your slice.
defineProps(
  getSliceComponentProps<Content.CoverageASlice>([
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
        class="grid lg:grid-cols-3 lg:bg-white lg:p-10 gap-4 my-4 rounded mx-6 text-[13px] lg:text-[16px] tracking-wide"
      >
        <div class="flex items-center">
          <div class="w-2 h-2 bg-[#18A56B] mr-4 lg:hidden"></div>
          <div>{{ slice.primary.coverage }}</div>
        </div>

        <div class="col-span-2 p-6 lg:p-0 bg-white">
          <PrismicRichText
            :field="slice.primary.description"
            :serializer="serializer"
          />
        </div>
      </div>
    </div>
  </section>
</template>
