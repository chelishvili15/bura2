<template>
  <div class="flex space-x-4 bg-gray-300 px-10 py-2">
    <button class="my-40" @click="wageba1">
      <p class="rotate-90 mb-20">წაღება</p>
      <p>{{ sum1 }}</p>
    </button>
    <div v-for="n in arr" class="cursor-pointer flex flex-col space-y-3">
      <img
        ref="card"
        :src="`/src/assets/aguri/${n}.png`"
        class="w-28 h-40"
        @click="click(n, $event)"
      />
      <img
        ref="card"
        :src="`/src/assets/guli/${n}.png`"
        class="w-28 h-40"
        @click="click(n, $event)"
      />
      <img
        ref="card"
        :src="`/src/assets/jvari/${n}.png`"
        class="w-28 h-40"
        @click="click(n, $event)"
      />
      <img
        ref="card"
        :src="`/src/assets/yvavi/${n}.png`"
        class="w-28 h-40"
        @click="click(n, $event)"
      />
    </div>
    <button class="my-40" @click="wageba2">
      <p class="rotate-90 mb-20">წაღება</p>
      <p>{{ sum2 }}</p>
    </button>
  </div>
</template>

<script setup>
import { ref } from "vue";

const card = ref(null);
const sum1 = ref(0);
const sum2 = ref(0);
const sum = ref(0);
const arr = ref([6, 7, 8, 9, 10, 11, 12, 13, 14]);

const click = (n, e) => {
  if (!e.target.classList.contains("opacity-20")) {
    e.target.classList.add("opacity-20");
    sum.value += n > 11 ? n % 10 : n < 10 ? 0 : n;
  }
};

const washla = () => {
  card.value.map((val) => {
    if (val.classList.contains("opacity-20")) {
      val.classList.remove("opacity-20");
      val.classList.add("opacity-0");
    }
  });
};

const wageba1 = () => { 
  sum1.value += sum.value;
  sum.value = 0;
  washla();
};

const wageba2 = () => {
  sum2.value += sum.value;
  sum.value = 0;
  washla();
};
</script>
