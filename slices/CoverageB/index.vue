<script setup lang="ts">
import { type Content } from "@prismicio/client";

// The array passed to `getSliceComponentProps` is purely optional.
// Consider it as a visual hint for you when templating your slice.
defineProps(
  getSliceComponentProps<Content.CoverageBSlice>([
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
    <div class="max-w-8xl container mx-6 mx-auto">
      <div class="my-4 grid gap-4 rounded px-6 lg:grid-cols-2">
        <div class="hidden lg:block">
          <!-- Empty content -->
        </div>
        <div class="grid grid-cols-2 gap-4 text-center">
          <div
            v-for="item in slice.primary.packages"
            :key="item.id"
            class="rounded-md bg-[#16A56B] py-4 text-white"
          >
            <p class="text-[10px] tracking-widest">{{ item.type }}</p>
            <p class="text-[13px] font-normal tracking-widest">
              {{ item.name }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
