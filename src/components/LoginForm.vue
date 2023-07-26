<template>
  <Card 
    btnColor="#8900EB"
    bgColor="#a024f9"
    title="登入框"
    btnText="登入"
    :action="signup"
  />
</template>

<script setup>
import Card from './common/_Card.vue';
import { auth } from '../firebase/init.js';
import { signInWithEmailAndPassword } from 'firebase/auth'
import { defineEmits } from 'vue'; 

const emit = defineEmits(['login']);
const signup = (email, password) => {
  // 註冊成功後，會自動登入
  signInWithEmailAndPassword(auth, email, password)
    .then((credential) => {
      console.log(credential.user)
      alert('登入成功')
    })
    .then(() => {
      console.log(auth.currentUser);
      emit('login');
    })
    .catch((error) => {
      alert(error.message)
    })
}

</script>

<style>
</style>