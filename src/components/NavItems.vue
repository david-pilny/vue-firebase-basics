<script setup>
import { useCurrentUser, useFirebaseAuth } from 'vuefire'
import BaseButton from './base/BaseButton.vue'
import { signOut } from 'firebase/auth'

const user = useCurrentUser()
console.log(user)

const auth = useFirebaseAuth()

async function signOutOfFirebase() {
  signOut(auth)
    .then(() => {
      // Sign-out successful.
      console.log("You're logged out")
    })
    .catch((error) => {
      // An error happened.
    })
}
</script>

<template>
  <nav class="pr-4">
    <BaseButton to="/">Home</BaseButton>
    <BaseButton to="/new">New</BaseButton>
    <BaseButton @click="signOutOfFirebase" v-if="user?.email"
      >Sign Out</BaseButton
    >
    <BaseButton v-else to="/sign-in">Sign-In</BaseButton>
  </nav>
</template>
