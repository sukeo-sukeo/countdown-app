<script setup>
import AppDiscription from './AppDiscription.vue';

const emits = defineEmits([
  "dialog-close"
])

</script>

<template>
  <div class="modal" @click="emits('dialog-close')"></div>
  <v-card class="modal-content">
    <AppDiscription />
    <v-card-actions>
      <v-spacer></v-spacer>
      <v-btn text @click="emits('dialog-close')"> 閉じる </v-btn>
    </v-card-actions>
  </v-card>
</template>

<style scoped>
.modal {
  z-index: 100;
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  background-color: rgba(0,0,0,.5);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.modal-content {
  z-index: 101;
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: rgba(0,0,0,.5);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  
   /* モーダルの幅や色などはお好きにどうぞ！ */
  background-color: white;
  width: 95%;
  height: auto;
  border-radius: 20px;
  padding: 10px;
  
}

</style>