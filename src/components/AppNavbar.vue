<script setup>
import NavItems from './NavItems.vue'
</script>

<template>
  <v-app-bar color="grey-darken-4" height="80">
    <div class="nav-title" @click="$router.push('/')">Kinkify</div>
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
}
.nav-title:hover {
  cursor: pointer;
  transform: scale(1.2);
}
</style>
