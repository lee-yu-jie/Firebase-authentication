<template>
  <Card 
    btnColor="#007508"
    bgColor="#00940A"
    title="註冊框"
    btnText="註冊"
    :action="signup"
  />
</template>

<script setup>
import Card from './common/_Card.vue';
import { auth } from '../firebase/init.js';
import { createUserWithEmailAndPassword, updateProfile } from 'firebase/auth'
import { defineEmits } from 'vue'; 

const emit = defineEmits(['login']);
const signup = (email, password) => {
  // 註冊成功後，會自動登入
  createUserWithEmailAndPassword(auth, email, password)
    .then((credential) => {
      console.log(credential.user)
      alert('註冊成功')
      updateProfile(auth.currentUser, {
        displayName: ''
      })
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

<script setup>
</script>

<style>
</style>