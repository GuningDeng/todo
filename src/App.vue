<!--
<v-app>: is a fundamental component that serves as the root element for a Vuetify application.
<v-main>: is a component that is used to define the main content area of application.
<router-view />: Vue Router.
-->
<template>
  <v-app>
    <nav-bar />
    <v-main>
      <router-view />
    </v-main>
    
  </v-app>
</template>

<script lang="ts" setup>
  //
</script>
