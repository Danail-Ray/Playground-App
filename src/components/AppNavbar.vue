<script setup>
import NavItems from './NavItems.vue'
</script>

<template>
  <v-app-bar color="teal">
    <v-app-bar-title class="nav-title">Playground</v-app-bar-title>
    <v-spacer></v-spacer>
    <NavItems />
  </v-app-bar>
</template>

<style>
.nav-title {
  font-family: 'Pacifico', cursive;
  padding: 1rem;
}
</style>
