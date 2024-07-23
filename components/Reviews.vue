<script setup lang="ts">
import { components } from "~/slices";

const prismic = usePrismic();
const { data: reviews } = useAsyncData("reviews", () =>
  prismic.client.getSingle("reviews")
);
</script>

<template>
  <!-- {{ page }} -->
  <section>
    <div class="container mx-auto max-w-3xl flex justify-center py-20 px-6">
      <SliceZone
        wrapper="main"
        :slices="reviews?.data.slices ?? []"
        :components="components"
      />
    </div>
  </section>
</template>
