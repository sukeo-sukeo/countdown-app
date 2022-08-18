<script setup>
import { ref } from "@vue/reactivity";

const emits = defineEmits([
  "login-click", "logout-click", "info-click"
]);

const props = defineProps({
  isLogin: String
});

</script>

<template>
  <v-app-bar class="select-none">
    <v-app-bar-title>
      <span class="cursor-pointer">カウントダウン.web</span>
    </v-app-bar-title>
    <template v-if="props.isLogin">
      <v-btn icon @click="emits('logout-click')">
        <v-icon>mdi-logout</v-icon>
      </v-btn>
    </template>
    <template v-else>
      <v-btn icon @click="emits('login-click')">
        <v-icon>mdi-account-circle-outline</v-icon>
      </v-btn>
    </template>
    <v-btn icon @click="emits('info-click')">
      <v-icon>mdi-information-outline</v-icon>
    </v-btn>
  </v-app-bar>
</template>