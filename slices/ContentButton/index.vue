<script lang="ts">
import { defineComponent } from "vue";
import { type Content } from "@prismicio/client";

export default defineComponent({
  props: getSliceComponentProps<Content.ContentButtonSlice>([
    "slice",
    "index",
    "slices",
    "context",
  ]),
  methods: {
    goBack() {
      this.$router.back();
    },
  },
});
</script>

<template>
  <section
    :data-slice-type="slice.slice_type"
    :data-slice-variation="slice.variation"
  >
    <div class="max-w-8xl container mx-auto mt-10 flex justify-between px-6">
      <div class="flex items-center">
        <!-- <img src="/img/icons/pdf.svg" class="mr-4 h-10 w-10" />
        <p class="text-[13px] tracking-wide md:text-[16px]">
          <PrismicLink :field="slice.primary.link">
            {{ slice.primary.text }}
          </PrismicLink>
        </p> -->
        <img src="/img/icons/pdf.svg" class="mr-4 h-8 w-8" />
        <a :href="slice.primary.link.url" download>
          <p class="text-[14px]">{{ slice.primary.text }}</p>
        </a>
        <!-- <a
          :href="slice.primary.link.url"
          class="rounded-md bg-[#18a56b] px-6 py-3 text-xs uppercase tracking-wide text-white"
          download
        >
          Pobierz OWU
        </a> -->
      </div>
      <button
        class="rounded-md bg-[#18a56b] px-6 py-3 text-xs uppercase tracking-wide text-white"
        @click="goBack"
      >
        {{ slice.primary.label }}
      </button>
    </div>
  </section>
</template>
