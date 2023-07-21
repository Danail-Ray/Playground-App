<script setup>
import NavItems from './NavItems.vue'
</script>

<template>
  <v-app-bar color="grey-darken-4" height="80">
    <router-link to="/" class="nav-title">Kinkify</router-link>
    <v-spacer></v-spacer>
    <NavItems />
  </v-app-bar>
</template>

<style scoped>
.nav-title {
  font-family: 'Pacifico', cursive;
  font-size: 1.3rem;
  transition: transform 0.9s ease-out;
  padding: 2rem;
  color: white;
}
.nav-title:hover {
  cursor: pointer;
  transform: scale(1.2);
}
</style>
