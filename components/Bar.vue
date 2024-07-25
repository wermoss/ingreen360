<template>
  <div class="absolute z-10 w-full">
    <div class="justify-left flex h-screen items-center">
      <div class="max-w-8xl container mx-auto w-full">
        <div class="flex">
          <ul class="flex flex-col gap-4">
            <li
              @click="moveHighlight(0)"
              :class="
                highlightIndex === 0
                  ? 'cursor-pointer bg-[#18a56b] text-white'
                  : 'cursor-pointer'
              "
              class="inline-block rounded-md px-4 py-2 text-sm"
            >
              3
            </li>
            <li
              @click="moveHighlight(1)"
              :class="
                highlightIndex === 1
                  ? 'cursor-pointer bg-[#18a56b] text-white'
                  : 'cursor-pointer'
              "
              class="inline-block rounded-md px-4 py-2 text-sm"
            >
              Y
            </li>
            <li
              @click="moveHighlight(2)"
              :class="
                highlightIndex === 2
                  ? 'cursor-pointer bg-[#18a56b] text-white'
                  : 'cursor-pointer'
              "
              class="inline-block rounded-md px-4 py-2 text-sm"
            >
              S
            </li>
            <li
              @click="moveHighlight(3)"
              :class="
                highlightIndex === 3
                  ? 'cursor-pointer bg-[#18a56b] text-white'
                  : 'cursor-pointer'
              "
              class="inline-block rounded-md px-4 py-2 text-sm"
            >
              X
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>
