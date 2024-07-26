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
  ]),
);
</script>

<template>
  <section
    :data-slice-type="slice.slice_type"
    :data-slice-variation="slice.variation"
  >
    <div class="container mx-auto my-10 px-6 text-[15px]">
      <div class="grid gap-20 lg:grid-cols-2">
        <div>
          <div class="flex flex-col">
            <div class="">
              <p
                class="mb-6 inline-block bg-[#18a56b] px-6 py-2 text-lg tracking-wider text-white"
              >
                {{ slice.primary.title }}
              </p>
            </div>

            <div
              v-for="item in slice.primary.additional_informations"
              class="mb-3 flex flex-row justify-center"
            >
              <div class="mr-4">
                <div
                  class="flex h-[30px] w-[30px] items-center justify-center rounded-full bg-[#00000015] text-sm"
                >
                  {{ item.number }}
                </div>
              </div>

              <div>
                <PrismicRichText
                  :field="item.text"
                  :serializer="serializer"
                  class="mt-1"
                />
              </div>
            </div>
          </div>
        </div>
        <div>
          <PrismicRichText
            :field="slice.primary.frame"
            :serializer="serializer"
            class="rounded-md bg-[#00000008] p-10"
          />
        </div>
      </div>
    </div>
  </section>
</template>
