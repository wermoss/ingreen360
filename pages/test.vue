<template>
  <section>
    <div class="flex h-screen w-screen flex-col items-center justify-between">
      <div class="absolute z-20">
        <div class="container mx-auto max-w-6xl">
          <ul class="flex w-[800px] flex-row text-center">
            <li
              :class="
                highlightIndex === 0
                  ? 'cursor-default bg-white'
                  : 'cursor-default'
              "
              class="h-screen px-10"
            >
              <div class="group" @mouseenter="fadeIn" @mouseleave="fadeOut">
                <div
                  class="change cursor-pointer py-6"
                  @click="moveHighlight(0)"
                >
                  Model 3
                </div>
                <div
                  ref="highlightBar0"
                  :class="{
                    highlightBar: true,
                    'always-visible': highlightIndex === 0,
                  }"
                  class="h-1 w-full bg-[#18a56b]"
                ></div>
              </div>
            </li>
            <li
              :class="
                highlightIndex === 1
                  ? 'cursor-default bg-white'
                  : 'cursor-default'
              "
              class="px-10"
            >
              <div class="group" @mouseenter="fadeIn" @mouseleave="fadeOut">
                <div
                  class="change cursor-pointer py-6"
                  @click="moveHighlight(1)"
                >
                  Model Y
                </div>
                <div
                  ref="highlightBar1"
                  :class="{
                    highlightBar: true,
                    'always-visible': highlightIndex === 1,
                  }"
                  class="h-1 w-full bg-[#18a56b]"
                ></div>
              </div>
            </li>
            <li
              :class="
                highlightIndex === 2
                  ? 'cursor-default bg-white'
                  : 'cursor-default'
              "
              class="px-10"
            >
              <div class="group" @mouseenter="fadeIn" @mouseleave="fadeOut">
                <div
                  class="change cursor-pointer py-6"
                  @click="moveHighlight(2)"
                >
                  Model S
                </div>
                <div
                  ref="highlightBar2"
                  :class="{
                    highlightBar: true,
                    'always-visible': highlightIndex === 2,
                  }"
                  class="h-1 w-full bg-[#18a56b]"
                ></div>
              </div>
            </li>
            <li
              :class="
                highlightIndex === 3
                  ? 'cursor-default bg-white'
                  : 'cursor-default'
              "
              class="px-10"
            >
              <div class="group" @mouseenter="fadeIn" @mouseleave="fadeOut">
                <div
                  class="change cursor-pointer py-6"
                  @click="moveHighlight(3)"
                >
                  Model X
                </div>
                <div
                  ref="highlightBar3"
                  :class="{
                    highlightBar: true,
                    'always-visible': highlightIndex === 3,
                  }"
                  class="h-1 w-full bg-[#18a56b]"
                ></div>
              </div>
            </li>
          </ul>
        </div>
      </div>
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
      <div class="max-w-8xl container mx-auto">
        <div class="grid grid-cols-2">
          <div>
            <div>
              <div class="image bg-red-100 p-40" v-if="highlightIndex === 0">
                A
              </div>
              <div
                class="image bg-yellow-100 p-40"
                v-else-if="highlightIndex === 1"
              >
                B
              </div>
              <div
                class="image bg-blue-100 p-40"
                v-else-if="highlightIndex === 2"
              >
                C
              </div>
              <div
                class="image bg-green-100 p-40"
                v-else-if="highlightIndex === 3"
              >
                D
              </div>
            </div>
          </div>
          <div>
            <div>
              <div class="bg-red-100 p-40" v-if="highlightIndex === 0">1</div>
              <div class="bg-yellow-100 p-40" v-else-if="highlightIndex === 1">
                2
              </div>
              <div class="bg-blue-100 p-40" v-else-if="highlightIndex === 2">
                3
              </div>
              <div class="bg-green-100 p-40" v-else-if="highlightIndex === 3">
                4
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import { gsap } from "gsap";

export default {
  data() {
    return {
      highlightIndex: 0,
    };
  },
  mounted() {
    this.moveHighlight(0); // Ustawienie domyślnego zaznaczenia na indeks 0
  },
  methods: {
    moveHighlight(index) {
      const lis = this.$el.querySelectorAll("li");
      const previousHighlightBar =
        this.$refs[`highlightBar${this.highlightIndex}`];
      const newHighlightBar = this.$refs[`highlightBar${index}`];

      if (previousHighlightBar) {
        previousHighlightBar.classList.remove("always-visible");
        gsap.to(previousHighlightBar, { duration: 0.5, opacity: 0 });
      }

      if (newHighlightBar) {
        newHighlightBar.classList.add("always-visible");
        gsap.to(newHighlightBar, { duration: 0.5, opacity: 1 });
      }

      if (this.highlightIndex !== null) {
        gsap
          .to(lis[this.highlightIndex], {
            backgroundColor: "#FFFFFF00",
            duration: 0.01,
            ease: "power1.inOut",
          })
          .then(() => {
            gsap.to(lis[index], {
              backgroundColor: "#f5f5f5",
              duration: 0.01,
              ease: "power1.inOut",
            });
          });
        this.highlightIndex = index;
      } else {
        gsap.to(lis[index], {
          backgroundColor: "#f5f5f5",
          duration: 0.01,
          ease: "power1.inOut",
        });
        this.highlightIndex = index;
      }
    },
    fadeIn(event) {
      const highlightBar = event.currentTarget.querySelector(".highlightBar");
      if (!highlightBar.classList.contains("always-visible")) {
        gsap.to(highlightBar, { duration: 0.5, opacity: 1 });
      }
    },
    fadeOut(event) {
      const highlightBar = event.currentTarget.querySelector(".highlightBar");
      if (!highlightBar.classList.contains("always-visible")) {
        gsap.to(highlightBar, { duration: 0.5, opacity: 0 });
      } else {
        gsap.to(highlightBar, { duration: 0, opacity: 1 });
      }
    },
  },
};
</script>

<style scoped>
.hidden {
  opacity: 0;
}
.highlightBar {
  opacity: 0;
}
.always-visible {
  opacity: 1 !important;
}
ul {
  list-style: none;
  padding: 0;
  margin: 0;
}
li {
  width: 100%;
}
</style>
