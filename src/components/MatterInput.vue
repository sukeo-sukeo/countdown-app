<script setup>

</script>

<template>
  <v-container>
    <v-row>
      <v-text-field
      label="事柄"
      placeholder="カウントダウンしたい事柄を入力してください"
      variant="outlined"
      ></v-text-field>
    </v-row>
    <v-row>
      <v-text-field
      label="実施日"
      placeholder="yyyy-mm-dd"
      variant="outlined"
      append-icon="mdi-calendar-range"
      ></v-text-field>
      <v-btn class="mt-2 mx-3">
        登録！
      </v-btn>
    </v-row>
  </v-container>
</template>

<style>
/* .v-text-field input {
  font-size: 10px;
  } */
</style>