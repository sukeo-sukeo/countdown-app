<script setup>
const props = defineProps({
  currentNum: Number,
  dataLength: Number
});
const emits = defineEmits([
  "matter-change"
]);

</script>

<template>
  <v-container>
    <v-row class="justify-space-around">
      <v-icon @click="emits('matter-change', -1)">
        mdi-arrow-expand-left
      </v-icon>
      <span @click="emits('matter-change', 0)">
        {{props.currentNum}}/{{props.dataLength}}
      </span>
      <v-icon @click="emits('matter-change', 1)">
        mdi-arrow-expand-right
      </v-icon>
    </v-row>
  </v-container>
</template>