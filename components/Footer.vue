<script setup lang="ts">
const prismic = usePrismic();
const { data: bbb } = useAsyncData("bbb", () =>
  prismic.client.getSingle("company"),
);
</script>

<template>
  <section class="bg-[#393A3A] py-20 text-white">
    <div class="max-w-8xl container mx-auto">
      <div class="mx-6 grid gap-10 md:grid-cols-2 lg:grid-cols-4">
        <div class="text-md tracking-wider">
          <PrismicImage :field="bbb?.data.monochrome_logo" class="h-[70px]" />
          <p>{{ bbb?.data.company_name }}</p>
          <p>{{ bbb?.data.address }}</p>
          <p>{{ bbb?.data.postcode }} {{ bbb?.data.town }}</p>
          <p>{{ bbb?.data.telephone_number }}</p>
          <p>{{ bbb?.data.email_address }}</p>
        </div>
        <div class="text-md tracking-wider">
          <p class="mb-4 uppercase tracking-[0.2em]">Nasze oddziały</p>
          <p class="text-gray-300">{{ bbb?.data.first_company_branch }}</p>
          <div v-for="item in bbb?.data.fcb_telephone_numbers">
            <ul>
              <li class="text-gray-300">{{ item.fcb_telephone_number }}</li>
            </ul>
          </div>
          <p class="mt-4">
            {{ bbb?.data.second_company_branch }}
          </p>
          <div v-for="item in bbb?.data.scb_telephone_numbers">
            <ul>
              <li>{{ item.scb_telephone_number }}</li>
            </ul>
          </div>
        </div>
        <FooterLinks />
      </div>
    </div>
  </section>
</template>
