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
  ]),
);
</script>

<template>
  <section
    :data-slice-type="slice.slice_type"
    :data-slice-variation="slice.variation"
  >
    <div class="max-w-8xl container mx-auto">
      <div
        class="mx-6 my-4 grid gap-4 rounded text-[13px] tracking-wide lg:grid-cols-3 lg:bg-white lg:p-10 lg:text-[16px]"
      >
        <div class="flex items-start">
          <div class="mr-4 h-2 w-2 bg-[#18A56B] lg:hidden"></div>
          <div>{{ slice.primary.coverage }}</div>
        </div>

        <div class="col-span-2 bg-white p-6 lg:p-0">
          <PrismicRichText
            :field="slice.primary.description"
            :serializer="serializer"
          />
        </div>
      </div>
    </div>
  </section>
</template>
