<script setup lang="ts">
const prismic = usePrismic();
const { data: ccc } = useAsyncData("ccc", () =>
  prismic.client.getSingle("footer"),
);
</script>

<template>
  <!-- {{ ccc }} -->
  <div class="text-md tracking-wider">
    <p class="mb-4 uppercase tracking-[0.2em]">
      {{ ccc?.data.first_column_name }}
    </p>
    <div v-for="item in ccc?.data.first_column">
      <ul>
        <li>
          <PrismicLink :field="item.link">{{ item.label }}</PrismicLink>
        </li>
      </ul>
    </div>
  </div>
  <div>
    <p class="mb-4 uppercase tracking-[0.2em]">
      {{ ccc?.data.second_column_name }}
    </p>
    <div v-for="item in ccc?.data.second_column">
      <ul>
        <li>
          <PrismicLink :field="item.link">{{ item.label }}</PrismicLink>
        </li>
      </ul>
    </div>
  </div>
</template>
