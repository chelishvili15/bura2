<template>
  <div>
    <div class="flex space-x-4 bg-gradient-to-l from-cyan-200 to-blue-500 px-10 py-4 rounded-2xl">
      <LongButton class="my-20" @click="wageba1">
        <span>{{ sum1 }}</span>
      </LongButton>
      <div v-for="n in arr" class="cursor-pointer flex flex-col space-y-3">
        <img
          v-for="cveti in cvet"
          ref="card"
          :src="getImageUrl(n, cveti)"
          class="w-20 h-32"
          @click="click(n, $event)"
        />
      </div>
      <LongButton class="my-20" @click="wageba2">
        <span>{{ sum2 }}</span>
      </LongButton>
    </div>
    <div class="mt-10 flex justify-between w-full">
      <Button @click="changeMode"
        >{{ card_3 ? "5" : "3" }} card</Button
      >
      <div class="flex gap-4">
        <Button @click="undo">Undo</Button>
        <Button class="from-red-400 to-red-600 text-gray-200" @click="reset">Reset</Button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import Button from "./Button.vue";
import LongButton from "./LongButton.vue"

const card = ref(null);
const card_3 = ref(false);
const sum1 = ref(0);
const sum2 = ref(0);
const sum = ref(0);
const arr = ref([6, 7, 8, 9, 10, 11, 12, 13, 14]);
const cvet = ref(["guli", "aguri", "jvari", "yvavi"]);

const getImageUrl = (n, cveti) => {
  return `${cveti}/${n.toString()}.png`;
};

const click = (n, e) => {
  if (
    !e.target.classList.contains("opacity-20") &&
    !e.target.classList.contains("opacity-0")
  ) {
    e.target.classList.remove("opacity-100");
    e.target.classList.add("opacity-20");
    sum.value += n > 11 ? n % 10 : n < 10 ? 0 : n;
  } else if (e.target.classList.contains("opacity-20")) {
    e.target.classList.remove("opacity-20");
    e.target.classList.add("opacity-100");
    sum.value -= n > 11 ? n % 10 : n < 10 ? 0 : n;
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

const undo = () => {
  card.value.map((val) => {
    if (val.classList.contains("opacity-20")) {
      val.classList.remove("opacity-20");
      val.classList.add("opacity-100");
    }
  });
};

const reset = () => {
  card.value.map((val) => {
    val.classList.remove("opacity-0");
    val.classList.remove("opacity-20");
    val.classList.remove("opacity-100");
    val.classList.add("opacity-100");
  });
  sum.value = 0;
  sum1.value = 0;
  sum2.value = 0;
};

const changeMode = () => {
  reset();
  card_3.value = !card_3.value;
  arr.value = card_3.value
    ? [10, 11, 12, 13, 14]
    : [6, 7, 8, 9, 10, 11, 12, 13, 14];
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
