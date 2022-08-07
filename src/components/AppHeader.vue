<script setup>

const dialog = () => alert("ダイアログ");

</script>

<template>
  <v-app-bar class="select-none">
    <v-app-bar-title>
      <span class="cursor-pointer">カウントダウン.web</span>
    </v-app-bar-title>
    <v-btn icon @click="dialog">
    <!-- <v-btn icon @click="dialog = true"> -->
      <v-icon>mdi-information-outline</v-icon>
    </v-btn>
  </v-app-bar>
</template>