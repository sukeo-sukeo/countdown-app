<script setup>

const props = defineProps({
  dataList: Array
});

</script>

<template>
<v-list class="w-100">
  <h3 class="text-center">期限いちらん</h3>
  <v-list-item v-for="data in props.dataList" :key="data">
    <span class="text-caption">
      {{data.matter}}
    </span>
    <span class="float-right">
      {{data.limit}}
    </span>
    <v-divider></v-divider>
  </v-list-item>
</v-list>
</template>