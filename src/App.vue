<script setup>
import { ref } from 'vue'
import SignIn from '/src/components/Sign-in.vue'
import SignUp from '/src/components/Sign-up.vue'

const showSigninModal = ref(false)
const showSignupModal = ref(false)

function showSignIn() {
  showSigninModal.value = true
}
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="50" height="50" />

    <nav>
      <a to="/">Home</a>

      <a to="/about">About</a>

      <button class="" @click="showSignIn">sign in</button>
      <button class="" @click="showSignupModal = true">sign up</button>
    </nav>
  </header>

  <main>
    <Teleport to="body">
      <SignIn :open="showSigninModal" @closeSignin="showSigninModal = false" />
      <SignUp :open="showSignupModal" @closeSignup="showSignupModal = false" />
    </Teleport>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
  display: flex;
  justify-content: space-between;
}

nav {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

button {
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 0.25rem;
  background-color: #333;
  color: white;
}

@media (min-width: 1024px) {
  header {
    display: flex;
  }

  .logo {
    margin: 0 2rem 0 0;
  }
}
</style>
