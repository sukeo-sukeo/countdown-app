<script setup>
import AppHeader from './components/AppHeader.vue';
import MatterInput from './components/MatterInput.vue';
import CountDown from './components/CountDown.vue';
import AppFooter from './components/AppFooter.vue';
import PagenationBtn from './components/PagenationBtn.vue';

</script>

<template>
  <v-app>
    <v-main>
      <AppHeader />
      <MatterInput class="mt-5" />
      <CountDown />
      <PagenationBtn />
      <AppFooter />
    </v-main>
  </v-app>
</template>