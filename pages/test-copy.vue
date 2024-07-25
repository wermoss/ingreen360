<template>
  <section>
    <div class="flex h-screen w-screen flex-col items-center justify-between">
      <div>
        <ul class="absolute z-20 flex flex-row">
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
                class="change cursor-pointer bg-pink-100 p-4"
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
                class="change cursor-pointer bg-pink-100 p-4"
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
                class="change cursor-pointer bg-pink-100 p-4"
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
                class="change cursor-pointer bg-pink-100 p-4"
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
      <!-- Nowy zestaw elementów li jako drugie przełączniki -->
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
      <div>
        <div>A</div>
        <div>B</div>
        <div>C</div>
        <div>D</div>
      </div>
      <div>c</div>
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
            duration: 1,
            ease: "power1.inOut",
          })
          .then(() => {
            gsap.to(lis[index], {
              backgroundColor: "#D1D5DB",
              duration: 1,
              ease: "power1.inOut",
            });
          });
        this.highlightIndex = index;
      } else {
        gsap.to(lis[index], {
          backgroundColor: "#D1D5DB",
          duration: 1,
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
