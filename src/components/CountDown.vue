<script setup>
import { ref } from "@vue/reactivity"
import { watch } from "@vue/runtime-core";

const props = defineProps({
  item: Object
});

</script>

<template>
  <v-container class="pt-0">
    <v-card>
      <v-table>
        <tbody>
          <tr>
            <td>事柄</td>
            <td>{{ props.item.matter }}</td>
          </tr>
          <tr>
            <td>実施日</td>
            <td>{{ props.item.date }}</td>
          </tr>
        </tbody>
      </v-table>
      <v-row class="justify-center align-baseline">
        <span class="text-h4">あと</span>
        <p style="font-size: 150px;">
          {{ props.item.count }}
        </p>
        <span class="text-h4 ms-3">日</span>
      </v-row>
    </v-card>
  </v-container>
</template>