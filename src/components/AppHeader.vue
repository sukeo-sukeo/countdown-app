<script setup>
import { ref, toRefs } from "@vue/reactivity";
import { watch } from "@vue/runtime-core";

const emits = defineEmits([
  "login-click", "logout-click", "info-click"
]);

const props = defineProps({
  isLogin: String,
  photoUrl: String
});

const photoURL = ref("")
const { photoUrl } = toRefs(props);
watch(photoUrl, () => photoURL.value = photoUrl.value)

</script>

<template>
  <v-app-bar class="select-none" color="indigo">
    <v-app-bar-title>
      <span class="cursor-pointer font-weight-bold">カウントダウン.web</span>
    </v-app-bar-title>
    <template v-if="props.isLogin">
      <v-btn icon @click="emits('logout-click')">
        <v-avatar>
          <img :src="photoURL" class="w-100">
        </v-avatar>
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