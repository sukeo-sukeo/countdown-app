<script setup>
import AppHeader from './components/AppHeader.vue';
import MatterInput from './components/MatterInput.vue';
import CountDown from './components/CountDown.vue';
import AppFooter from './components/AppFooter.vue';
import PagenationBtn from './components/PagenationBtn.vue';
import { ref } from '@vue/reactivity';

const sampleData = [
  { matter: "test1", date: "2022-12-25", count: 60 },
  { matter: "test2", date: "2022-12-25", count: 20 },
  { matter: "test3", date: "2022-12-25", count: 10 },
  { matter: "test4", date: "2022-12-25", count: 10 },
  { matter: "test5", date: "2022-12-25", count: 10 },
  { matter: "test6", date: "2022-12-25", count: 10 },
];

const currentNum = ref(0);
const currentItem = ref({
  matter: "syoki",
  date: "yyyy-mm-dd",
  count: "00"
});
const pagenationHundle = (ope) => {
  if (ope === 0) {
    currentNum.value = 0
  } else {
    currentNum.value += ope;
  }

  if (currentNum.value < 0) currentNum.value = sampleData.length - 1;
  if (currentNum.value >= sampleData.length) currentNum.value = 0;

  currentItem.value = sampleData[currentNum.value];
}

</script>

<template>
  <v-app>
    <v-main>
      <AppHeader />
      <MatterInput class="mt-5" />
      <CountDown :item="currentItem" />
      <PagenationBtn 
      @matter-change="pagenationHundle" 
      :currentNum="currentNum + 1"
      :dataLength="sampleData.length" />
      <AppFooter />
    </v-main>
  </v-app>
</template>