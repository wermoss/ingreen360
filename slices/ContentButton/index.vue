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
    <div class="max-w-8xl container mx-auto mt-10 flex justify-end px-6">
      <button
        class="rounded-md bg-[#18a56b] px-6 py-3 text-xs uppercase tracking-wide text-white"
        @click="goBack"
      >
        {{ slice.primary.label }}
      </button>
    </div>
  </section>
</template>
