<script setup>
import { ref } from "@vue/reactivity"

const sampleData = [
  {matter: "test1", date:"yyyy-mm-dd", count: 60},
  {matter: "test2", date:"yyyy-mm-dd", count: 20},
  {matter: "test3", date:"yyyy-mm-dd", count: 10},
]

const matter = ref("基本情報技術者試験");
const date = ref("2022-10-24");
const count = ref(65);

</script>

<template>
  <v-container class="pt-0">
    <v-card>
      <v-table>
        <tbody>
          <tr>
            <td>事柄</td>
            <td>{{ matter }}</td>
          </tr>
          <tr>
            <td>実施日</td>
            <td>{{ date }}</td>
          </tr>
        </tbody>
      </v-table>
      <v-row class="justify-center align-baseline">
        <span class="text-h4">あと</span>
        <p style="font-size: 150px;">
          {{ count }}
        </p>
        <span class="text-h4 ms-3">日</span>
      </v-row>
    </v-card>
  </v-container>
</template>