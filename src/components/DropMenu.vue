<template>
  <v-spacer />
  <v-menu>
    <template v-slot:activator="{ props }">
      <v-btn icon v-bind="props" color="blue-lighten-5">
        <v-icon>mdi-dots-vertical</v-icon>
      </v-btn>
    </template>
    <v-list
      style="position: absolute; left: -100px; z-index: 999"
      color="white"
    >
     <v-list-item>
      hoge
     </v-list-item>
     <v-list-item>
      hoge
     </v-list-item>
     <v-list-item>
      hoge
     </v-list-item>
    </v-list>
  </v-menu>
</template>