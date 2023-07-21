<script setup>
import { ref, watchEffect } from 'vue'

const scrolledNav = ref(null)
const mobile = ref(null)
const mobileNav = ref(null)
const windowWidth = ref(null)

function toggleMobileNav() {
  mobileNav.value = !mobileNav.value
}

const checkScreen = () => {
  windowWidth.value = window.innerWidth
  if (windowWidth.value <= 750) {
    mobile.value = true
    return
  }
  mobile.value = false
  mobileNav.value = false
  return
}

const updateScroll = () => {
  const scrollPosition = window.scrollY
  if (scrollPosition > 50) {
    scrolledNav.value = true
    return
  }
  scrolledNav.value = false
}

// watching the window size for change
watchEffect(() => {
  window.addEventListener('resize', checkScreen)
  window.addEventListener('scroll', updateScroll)
})
</script>

<template>
  <header :class="{ 'scrolled-nav': scrolledNav }">
    <nav>
      <div class="branding">
        <img src="@/assets/logo.svg" alt="" />
        <router-link class="brandName" to="/">Kinkify</router-link>
      </div>
      <ul v-show="!mobile" class="navigation">
        <li><router-link class="link" to="/">Home</router-link></li>
        <li><router-link class="link" to="/new">New</router-link></li>
        <li><router-link class="link" to="/sign-in">Sign-In</router-link></li>
      </ul>
      <div class="icon">
        <i
          @click="toggleMobileNav"
          v-show="mobile"
          class="ri-menu-line"
          :class="{ 'icon-active': mobileNav }"
        ></i>
      </div>
      <transition name="mobile-nav">
        <ul v-show="mobileNav" class="dropdown-nav">
          <li><router-link class="link" to="/">Home</router-link></li>
          <li><router-link class="link" to="/new">New</router-link></li>
          <li><router-link class="link" to="/sign-in">Sign-In</router-link></li>
        </ul>
      </transition>
    </nav>
  </header>
</template>

<style scoped>
header {
  background-color: rgba(0, 0, 0, 0.8);
  z-index: 99;
  width: 100%;
  position: fixed;
  transition: 0.5s ease all;
  color: white;
}

nav {
  display: flex;
  position: relative;
  flex-direction: row;
  padding: 18px 0;
  transition: 0.5s ease all;
  width: 90%;
  margin: 0 auto;
}

@media (min-width: 1700px) {
  header nav {
    max-width: 1700px;
  }
}

ul,
.link {
  font-weight: 500;
  color: white;
  list-style: none;
  text-decoration: none;
}

li {
  text-transform: uppercase;
  padding: 16px;
  margin-left: 16px;
}

.link {
  font-size: 14px;
  transition: 0.5s ease all;
  padding-bottom: 4px;
  border-bottom: 1px solid transparent;
}

.link:hover {
  color: #00afea;
  border-color: #00afea;
}

.branding {
  display: flex;
  align-items: center;
  transition: 0.7s ease-out;
}

.branding:hover {
  transform: scale(1.1);
}

.branding img {
  width: 50px;
  transition: 0.7s ease all;
}

.branding .brandName {
  text-decoration: none;
  color: white;
  font-family: 'Pacifico', cursive;
  font-size: 1.3rem;
  padding-left: 1rem;
}

.navigation {
  display: flex;
  align-items: center;
  flex: 1;
  justify-content: flex-end;
}

.icon {
  display: flex;
  position: absolute;
  top: 0;
  align-items: center;
  right: 24px;
  height: 100%;
}

.icon i {
  cursor: pointer;
  font-size: 24px;
  transition: 0.8s ease all;
}

.icon-active {
  transform: rotate(180deg);
}

.dropdown-nav {
  display: flex;
  flex-direction: column;
  position: fixed;
  width: 100%;
  max-width: 250px;
  height: 100%;
  background-color: white;
  top: 0;
  left: 0;
}

.dropdown-nav li {
  margin-left: 0;
}
.dropdown-nav li .link {
  color: #000;
}

.mobile-nav-enter-active,
.mobile-nav-leave-active {
  transition: 1s ease all;
}

.mobile-nav-enter-from,
.mobile-nav-leave-to {
  transform: translateX(-250px);
}

.mobile-nav-enter-to {
  transform: translateX(0);
}

.scrolled-nav {
  background-color: #000;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1),
    0 2px 4px -1px rgba(0, 0, 0, 0.06);
}
.scrolled-nav nav {
  padding: 10px;
}
.scrolled-nav nav .branding img {
  width: 40px;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1),
    0 2px 4px -1px rgba(0, 0, 0, 0.06);
}
</style>
