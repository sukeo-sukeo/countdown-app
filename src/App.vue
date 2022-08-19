<script setup>
import AppHeader from './components/AppHeader.vue';
import MatterInput from './components/MatterInput.vue';
import CountDown from './components/CountDown.vue';
import AppFooter from './components/AppFooter.vue';
import PagenationBtn from './components/PagenationBtn.vue';

import AppDiscription from './components/AppDiscription.vue';
import AppDialog from './components/AppDialog.vue';

import { getAuth, signInWithPopup, signOut, onAuthStateChanged, GoogleAuthProvider } from "firebase/auth";
import { collection, getDocs, orderBy, query, where } from "firebase/firestore";
import { db } from './main.js';

import { ref } from '@vue/reactivity';

const dataList = ref([]);
const getData = async (update = 0) => {
  dataList.value = [];

  const q = query(collection(db, "matters"), where("userId", "==", isLogin.value), orderBy("created", "desc"));

  try {
    const docs = await getDocs(q);
    docs.forEach(doc => {
      const data = doc.data();
      data.itemId = doc.id;
      dataList.value.push(data);
    });

    currentNum.value = update ? currentNum.value : 0;
    currentItem.value = update ? dataList.value[currentNum.value] : dataList.value[0];
   
  } catch (e) {
    console.error("Error getting document: ", e);
  }
}

const currentNum = ref(0);
const currentItem = ref({});

const pagenationHundle = (ope) => {
  if (ope === 0) {
    currentNum.value = 0
  } else {
    currentNum.value += ope;
  }

  if (currentNum.value < 0) currentNum.value = dataList.value.length - 1;
  if (currentNum.value >= dataList.value.length) currentNum.value = 0;

  currentItem.value = dataList.value[currentNum.value];
}


const isLogin = ref(""); //login中はuidが入る
const showDialog = ref(false);

const auth = getAuth();
const provider = new GoogleAuthProvider();

onAuthStateChanged(auth, async (user) => {
  if (user) {
    isLogin.value = user.uid;
    await getData();
  }
});

const login = async () => {
  try {
    const result = await signInWithPopup(auth, provider);
    const user = result.user;
    isLogin.value = user.uid;
  } catch (error) {
    const errorCode = error.code;
    const errorMessage = error.message;
    const email = error.customData.email;
    const credential = GoogleAuthProvider.credentialFromError(error);
  }
};

const logout = async () => {
  if (confirm("ログアウトしてもよろしいですか？")) {
    await signOut(auth);
    isLogin.value = "";
    dataList.value = [];
  }
}


</script>

<template>
  <v-app>
    <v-main>
      <AppHeader
       :isLogin="isLogin"
       @login-click="login"
       @logout-click="logout"
       @info-click="showDialog = true" />
      
      <MatterInput class="mt-5"
       :isLogin="isLogin"
       @item-registed="getData" />

      <!-- v-if isLogin -->
      <template v-if="isLogin">
        <template v-if="dataList.length">
        <!-- データがある -->
          <CountDown 
          :item="currentItem"
          @delete-click="getData"
          @update-click="getData"/>
          <PagenationBtn 
          @matter-change="pagenationHundle" 
          :currentNum="currentNum + 1"
          :dataLength="dataList.length" />
        </template>
        <template v-else>
          <!-- データがない -->
          <h3 class="text-center">まずはデータを登録してください</h3>
        </template>
      </template>

      <template v-else>
        <AppDiscription />
      </template>

      <AppDialog 
      v-if="showDialog" 
      @dialog-close="showDialog = false">
        <AppDiscription />
      </AppDialog>
      
      <AppFooter />
    </v-main>
  </v-app>
</template>