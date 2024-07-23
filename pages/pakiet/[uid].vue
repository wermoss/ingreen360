<script setup>
import { usePrismic } from "@prismicio/vue";
import { useAsyncData, useRoute } from "nuxt/app";
import { components } from "~/slices";

const route = useRoute();
const { client } = usePrismic();

const { data: room } = await useAsyncData(`room-${route.params.uid}`, () =>
  client.getByUID("additional_package", route.params.uid)
);
</script>

<template>
  <section class="pt-40 pb-20 bg-[#F5F5F5]">
    <!-- {{ room }} -->
    <div class="container max-w-6xl mx-auto">
      <SliceZone
        wrapper="main"
        :slices="room?.data.slices ?? []"
        :components="components"
      />
    </div>
  </section>
  <Disclaimer />
  <Reviews />
</template>
