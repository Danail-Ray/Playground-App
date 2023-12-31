<script setup>
import { ref } from 'vue'
import { useFirebaseAuth } from 'vuefire'
import {
  createUserWithEmailAndPassword,
  signInWithEmailAndPassword,
} from '@firebase/auth'

const auth = useFirebaseAuth()
const userInput = ref({
  email: '',
  password: '',
})

async function createUser() {
  createUserWithEmailAndPassword(
    auth,
    userInput.value.email,
    userInput.value.password
  )
    .then((userCredential) => {
      // Signed in
      const user = userCredential.user
    })
    .catch((error) => {
      console.log(error.code, error.message)
    })
}

async function signInToFirebase() {
  signInWithEmailAndPassword(
    auth,
    userInput.value.email,
    userInput.value.password
  )
    .then((userCredential) => {
      // Signed in
      const user = userCredential.user
      console.log('You are logged in')
    })
    .catch((error) => {
      console.log(error.code, error.message)
    })
}

let inputType = ref('password')
let showPasswordIcon = ref('ri-eye-off-line')

function toggleShow() {
  inputType.value = inputType.value === 'password' ? 'text' : 'password'
  showPasswordIcon.value =
    showPasswordIcon.value === 'ri-eye-off-line'
      ? 'ri-eye-line'
      : 'ri-eye-off-line'
}
</script>

<template>
  <div class="background-img" :style="{ paddingTop: '100px' }">
    <div class="login">
      <form action="" class="login-form" @submit.prevent="">
        <h1 class="login-title">Login</h1>
        <div class="login-content">
          <div class="login-box">
            <i class="ri-user-3-line login-icon"></i>
            <div class="login-box-input">
              <input
                v-model="userInput.email"
                type="email"
                label="Email"
                required
                class="login-input"
                placeholder=" "
              />
              <label for="" class="login-label">E-Mail</label>
            </div>
          </div>

          <div class="login-box">
            <i class="ri-lock-2-line login-icon"></i>
            <div class="login-box-input">
              <input
                v-model="userInput.password"
                label="Password"
                :type="inputType"
                required
                class="login-input"
                placeholder=" "
              />
              <label for="" class="login-label">Password</label>
              <i
                @click="toggleShow"
                class="login-eye"
                :class="showPasswordIcon"
              ></i>
            </div>
          </div>
        </div>
        <div class="login-check">
          <div class="login-check-group">
            <input type="checkbox" class="login-check-input" />
            <label for="" class="login-check-label">Remember me</label>
          </div>

          <a href="#" class="login-forgot">Forgot Password?</a>
        </div>

        <button @click="signInToFirebase" class="login-button">Login</button>
        <p class="login-register">
          Don't have an account?
          <a @click="createUser" href="#">Create user with one click</a>
        </p>
      </form>
    </div>
  </div>
</template>

<style scoped>
/* google fonts */
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;500&display=swap');

* {
  box-sizing: border-box;
}

body,
input,
button {
  font-size: 1rem;
  font-family: 'Poppins', sans-serif;
}

input,
button {
  border: none;
  outline: none;
}
a {
  text-decoration: none;
}

.login {
  position: relative;
  height: 100%;
  display: grid;
  align-items: center;
  color: white;
}

.login-img {
  position: absolute;
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center;
}

.background-img {
  background-image: url('../assets/bg.avif');
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  width: 100%;
  height: 100%;
  position: fixed;
}
.login-form {
  position: relative;
  background-color: hsla(0, 0%, 100%, 0.1);
  border-radius: 1rem;
  border: 2px solid white;
  padding: 2.5rem 1.5rem;
  margin-inline: 1.5rem;
  backdrop-filter: blur(8px);
}
.login-title {
  text-align: center;
  font-size: 2rem;
  font-weight: 500;
  margin-bottom: 2rem;
}

.login-content,
.login-box {
  display: grid;
}
.login-content {
  row-gap: 1.75rem;
  margin-bottom: 1.5rem;
}
.login-box {
  grid-template-columns: max-content 1fr;
  align-items: center;
  column-gap: 0.75rem;
  border-bottom: 2px solid white;
}

.login-icon,
.login-eye {
  font-size: 1.25rem;
}
.login-input {
  width: 100%;
  padding-block: 0.8rem;
  background: none;
  color: white;
  position: relative;
  z-index: 1;
}

.login-box-input {
  position: relative;
}
.login-label {
  position: absolute;
  left: 0;
  top: 13px;
  font-weight: 500;
  transition: top 0.3s, font-size 0.3s;
}

.login-eye {
  position: absolute;
  right: 0;
  top: 18px;
  z-index: 10;
  cursor: pointer;
}

.login-box:nth-child(2) input {
  padding-right: 1.8rem;
}

.login-check,
.login-check-group {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.login-check {
  margin-bottom: 1.5rem;
}

.login-check-label,
.login-forgot,
.login-register {
  font-size: 0.813rem;
}

.login-check-group {
  column-gap: 0.5rem;
}

.login-check-input {
  width: 16px;
  height: 16px;
}

.login-forgot {
  color: white;
}

.login-forgot:hover {
  text-decoration: underline;
}

.login-button {
  width: 100%;
  padding: 1rem;
  border-radius: 0.5rem;
  background-color: white;
  font-weight: 500;
  cursor: pointer;
  margin-bottom: 2rem;
  color: black;
}
.login-register {
  text-align: center;
}

.login-register a {
  color: white;
  font-weight: 500;
}

.login-register a:hover {
  text-decoration: underline;
}

.login-input:focus + .login-label {
  top: -12px;
  font-size: 0.813rem;
}

.login-input:not(:placeholder-shown).login-input:not(:focus) + .login-label {
  top: -12px;
  font-size: 0.813rem;
}

/* media queries */

@media screen and (min-width: 576px) {
  .login {
    justify-content: center;
  }
  .login-form {
    width: 432px;
    padding: 4rem 3rem 3.5rem;
    border-radius: 1.5rem;
  }
}
</style>
