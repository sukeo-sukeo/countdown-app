<script setup>
import { ref } from "@vue/reactivity";
import { collection, addDoc, serverTimestamp } from "firebase/firestore";
import { db } from "../main.js";

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
    alert("ログインをお願いします。");
    return
  }

  if (values.length !== 2 ||
    values[0] === "" ||
    values[1] === "") {
    alert("入力が不足しています。");
    return
  }

  try {
    const docRef = await addDoc(collection(db, "matters"), item);
    console.log("Document written with ID: ", docRef.id);

    data.value = [];
    emits("item-registed");

  } catch (e) {
    console.error("Error adding document: ", e);
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
      label="実施日"
      placeholder="yyyy-mm-dd"
      variant="outlined"
      append-icon="mdi-calendar-range"
      v-model="data[1]"
      ></v-text-field>
      <v-btn class="mt-2 mx-3" @click="registData">
        登録！
      </v-btn>
    </v-row>
  </v-container>
</template>