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
  ])
);
</script>

<template>
  <section
    :data-slice-type="slice.slice_type"
    :data-slice-variation="slice.variation"
  >
    <div class="container mx-auto max-w-8xl mx-6">
      <div class="grid lg:grid-cols-2 px-6 gap-4 my-4 rounded">
        <div class="hidden lg:block">
          <!-- Empty content -->
        </div>
        <div class="grid grid-cols-2 text-center gap-4">
          <div
            v-for="item in slice.primary.packages"
            :key="item.id"
            class="bg-[#16A56B] py-4 rounded-md text-white"
          >
            <p class="text-[10px] tracking-widest">{{ item.type }}</p>
            <p class="font-normal text-[13px] tracking-widest">
              {{ item.name }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
