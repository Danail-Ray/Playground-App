<script setup>
import NavItems from './NavItems.vue'
</script>

<template>
  <v-app-bar color="grey-darken-4" height="80">
    <a class="nav-title" href="/">Kinkify</a>
    <v-spacer></v-spacer>
    <NavItems />
  </v-app-bar>
</template>

<style scoped>
a {
  text-decoration: none;
  color: white;
}

.nav-title {
  font-family: 'Pacifico', cursive;

  font-size: 1.3rem;
  transition: transform 0.9s ease-out;
  padding: 2rem;
}
a.nav-title:hover {
  transform: scale(1.2);
}
</style>
