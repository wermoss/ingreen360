<script setup lang="ts">
import { components } from "~/slices";

const prismic = usePrismic();
const { data: page } = useAsyncData("page", () =>
  prismic.client.getSingle("disclaimer")
);
</script>

<template>
  <!-- {{ page }} -->
  <section>
    <div class="container mx-auto max-w-6xl flex justify-center py-20 px-6">
      <SliceZone
        wrapper="main"
        :slices="page?.data.slices ?? []"
        :components="components"
      />
    </div>
  </section>
</template>
