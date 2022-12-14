<script setup>
import AppDialog from "./AppDialog.vue";
import { ref, toRefs } from "@vue/reactivity";
import { deleteDoc, doc, updateDoc } from "firebase/firestore";
import { db } from '../config/firebase.config.js';
import { computed, watch } from "@vue/runtime-core";

const props = defineProps({
  item: Object,
});
const emits = defineEmits([
  "delete-click", "update-click", "card-swipe", "swipe-show-list", "sort-limit", "sort-regist"
]);

const showDialog = ref(false);
const data = ref([]);

const { item } = toRefs(props);
watch(item, () => {
  data.value[0] = item.value.matter;
  data.value[1] = item.value.limit;
});

const getYMD = (dateObj) => {
  const Y = dateObj.getFullYear();
  const M = dateObj.getMonth() + 1;
  const D = dateObj.getDate();
  return `${Y}/${M}/${D}`;
}

const limitDay = computed(() => {
  let limit = new Date(item.value.limit);
  let today = new Date();

  limit = new Date(getYMD(limit) + " 00:00:00");
  today = new Date(getYMD(today));

  return Math.ceil((limit - today) / (1000 * 60 * 60 * 24)).toString();
});


const updateData = async () => {
  if (!data.value[0] || !data.value[1]) {
    alert("入力に不備あり！");
    return
  }

  try {
    await updateDoc(doc(db, "matters", props.item.itemId), {
      matter: data.value[0],
      limit: data.value[1]
    });
    emits("update-click", 1);
  
  } catch (e) {
    alert("update error:", e);
  }
}

const removeData = async () => {
  if (confirm("アイテムを削除します")) {
    try {
      await deleteDoc(doc(db, "matters", props.item.itemId));
      emits("delete-click");
    
    } catch (e) {
      alert("delete error: ", e);
    }
  }
}


</script>

<template>
  <v-container class="pt-0">
    <v-card class="slider" v-touch="{
      up: () => emits('swipe-show-list'),
      right: () => emits('card-swipe', -1),
      left: () => emits('card-swipe', 1),
      
    }">
      <v-table>
        <tbody>
          <tr>
            <td>事柄</td>
            <td>
              {{ item.matter }}
              <v-icon class="float-right" @click="showDialog = true">mdi-pencil</v-icon>
            </td>
          </tr>
          <tr>
            <td>実施日</td>
            <td>
              {{ item.limit }}
              <v-icon class="float-right" @click="showDialog = true">mdi-pencil</v-icon>
            </td>
          </tr>
        </tbody>
      </v-table>
      <v-row class="justify-center align-baseline">

        <v-btn elevation="0" icon style="position: absolute; left: 20px; margin-top: 20px;">
          <v-icon>mdi-dots-vertical</v-icon>
          <v-menu activator="parent">
            <v-list>
              <v-list-item @click="emits('sort-limit', 0, 'limit')">
                <v-icon>mdi-sort</v-icon>
                締切順
              </v-list-item>
              <v-list-item @click="emits('sort-regist', 0, 'created')">
                <v-icon>mdi-sort</v-icon>
                登録順
              </v-list-item>
              <v-list-item @click="removeData">
                <v-icon>mdi-delete</v-icon>
                削除
              </v-list-item>
            </v-list>
          </v-menu>
        </v-btn>

        <span class="text-h5">あと</span>
        <p class="text-indigo font-rubik" style="font-size: 100px;">
          {{ limitDay }}
        </p>
        <span class="text-h4 ms-3">日</span>
      </v-row>
    </v-card>

    <!-- 編集ダイアログ -->
    <!-- MatterInput.vueを流用 -->
    <AppDialog 
      v-if="showDialog" 
      @dialog-close="showDialog = false">
      <p class="mb-5">編集</p>
      <v-row class="w-100">
        <v-text-field
        :label="item.matter"
        variant="outlined"
        v-model="data[0]"
        ></v-text-field>
      </v-row>
      <v-row class="w-100">
        <v-text-field
        :label="item.limit"
        type="date"
        variant="outlined"
        v-model="data[1]"
        ></v-text-field>
        <v-btn class="mt-2 mx-3 bg-indigo" @click="updateData">
          変更する！
        </v-btn>
      </v-row>
    </AppDialog>

  </v-container>
</template>