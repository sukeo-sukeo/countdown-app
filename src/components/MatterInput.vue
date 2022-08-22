<script setup>
import { ref } from "@vue/reactivity";
import { collection, addDoc, serverTimestamp } from "firebase/firestore";
import { db } from "../config/firebase.config.js";

const props = defineProps({
  isLogin: String
});
const emits = defineEmits([
  "item-registed"
])

const data = ref([]);

const registData = async () => {
  const values = data.value;
 
  const item = {
      matter: values[0],
      limit: values[1],
      userId: props.isLogin,
      created: serverTimestamp()
    };

  if (!props.isLogin) {
    alert("ログインをお願いします。\nログインはGoogleアカウントでの簡単ログインに対応しています。");
    return
  }

  if (!values[0] || !values[1]) {
    alert("入力が不足しています。");
    return
  }

  try {
    const docRef = await addDoc(collection(db, "matters"), item);
    alert("アイテムを登録しました！");

    data.value = [];
    emits("item-registed");

  } catch (e) {
    alert("Error adding document: ", e);
  }
}

</script>

<template>
  <v-container class="pb-0">
    <v-row>
      <v-text-field
      label="事柄"
      placeholder="カウントダウンしたい事柄を入力してください"
      variant="outlined"
      v-model="data[0]"
      ></v-text-field>
    </v-row>
    <v-row>
      <v-text-field
      type="date"
      label="実施日"
      variant="outlined"
      v-model="data[1]"
      ></v-text-field>
      <v-btn class="mt-2 mx-3 bg-indigo" @click="registData">
        登録！
      </v-btn>
      
    </v-row>
  </v-container>
</template>