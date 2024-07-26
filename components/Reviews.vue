<script setup lang="ts">
import { components } from "~/slices";

const prismic = usePrismic();
const { data: reviews } = useAsyncData("reviews", () =>
  prismic.client.getSingle("reviews"),
);
</script>

<template>
  <!-- {{ page }} -->
  <section>
    <div class="container mx-auto flex max-w-5xl justify-center px-6 py-20">
      <SliceZone
        wrapper="main"
        :slices="reviews?.data.slices ?? []"
        :components="components"
      />
    </div>
  </section>
</template>
