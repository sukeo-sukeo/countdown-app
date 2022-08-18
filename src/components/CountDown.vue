<script setup>
import { ref } from "@vue/reactivity"

const props = defineProps({
  item: Object
});

const updateData = () => {

}

const removeData = () => {
  
}

</script>

<template>
  <v-container class="pt-0">
    <v-card>
      <v-table>
        <tbody>
          <tr>
            <td>事柄</td>
            <td>
              {{ props.item.matter }}
              <v-icon class="float-right" @click="updateData">mdi-logout</v-icon>
            </td>
          </tr>
          <tr>
            <td>実施日</td>
            <td>
              {{ props.item.limit }}
              <v-icon class="float-right" @click="updateData">mdi-logout</v-icon>
            </td>
          </tr>
        </tbody>
      </v-table>
      <v-row class="justify-center align-baseline">
        <v-btn icon style="position: absolute; left: 30px; margin-top: 55px;" @click="removeData">
          <v-icon>mdi-logout</v-icon>
        </v-btn>
        <span class="text-h4">あと</span>
        <p style="font-size: 150px;">
          {{ 10 }}
        </p>
        <span class="text-h4 ms-3">日</span>
      </v-row>
    </v-card>
  </v-container>
</template>