<template>
  <Loading v-if="isLoading"/>
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
import Loading from './common/_Loading.vue';
import { auth, db } from '../firebase/init.js';
import { createUserWithEmailAndPassword, updateProfile } from 'firebase/auth'
import { doc, setDoc } from 'firebase/firestore';
import { defineEmits, ref } from 'vue'; 

const emit = defineEmits(['login']);
const isLoading = ref(false);

const createEmptyInfo = async (id) => {
  const docRef = doc(db, "members", id);
  const emptyInfo = {
    userID: id,
    address: '',
    phone: ''
  }
  await setDoc(docRef, emptyInfo, { merge: true});
  emit('login');
  isLoading.value = false;
}


const signup = (email, password) => {
  // 註冊成功後，會自動登入
  isLoading.value = true;
  createUserWithEmailAndPassword(auth, email, password)
    .then((credential) => {
      console.log(credential.user)
      alert('註冊成功')
      updateProfile(auth.currentUser, {
        displayName: ''
      })
    })
    .then(() => {
      // console.log(auth.currentUser);
      createEmptyInfo(auth.currentUser.uid);
    })
    .catch((error) => {
      alert(error.message)
      isLoading.value = false;
    })
}

</script>

<style>
</style>

<script setup>
</script>

<style>
</style>