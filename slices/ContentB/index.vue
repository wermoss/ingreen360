<script setup lang="ts">
import { type Content } from "@prismicio/client";

const serializer = {
  heading2: ({ children }) =>
    `<h2 class="font-semibold text-lg mb-4 last:mb-0">${children}</h2>`,
  heading3: ({ children }) =>
    `<h3 class="font-semibold text-lg mb-4 last:mb-0">${children}</h3>`,
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
  getSliceComponentProps<Content.ContentBSlice>([
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
    <div class="container mx-auto px-6 my-10 text-[15px]">
      <div class="grid lg:grid-cols-2 gap-20">
        <div>
          <div class="flex flex-col">
            <div
              v-for="item in slice.primary.additional_informations"
              class="flex flex-row"
            >
              <div class="mr-4">{{ item.number }}</div>
              <div>
                <PrismicRichText :field="item.text" :serializer="serializer" />
              </div>
            </div>
          </div>
        </div>
        <div>
          <PrismicRichText
            :field="slice.primary.frame"
            :serializer="serializer"
            class="bg-gray-200 p-10 rounded-md"
          />
        </div>
      </div>
    </div>
  </section>
</template>
