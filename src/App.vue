<template>
  <v-app>
    <v-app-bar color='success' dark app>
      <v-toolbar-title>体調情報</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-toolbar-items>
        <v-btn text to="/">ホーム</v-btn>
        <v-btn text to="/editor">体温追加</v-btn>
      </v-toolbar-items>
    </v-app-bar>
    <v-content>
      <router-view />
    </v-content>
    <v-footer color='success' dark app class="justify-center">
      Taro watanabe
    </v-footer>

  </v-app>
</template>