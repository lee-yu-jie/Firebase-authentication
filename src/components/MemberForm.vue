<template>
  <Loading v-if="isLoading"/>
  <div class="member-form form-Box">
    <h2 class="title">會員資料</h2>
    <form @submit.prevent="submit">
      <div class="info">
        <label for="address">地址</label>
        <input type="text" placeholder="請輸入地址" v-model="address" id="address" :disabled="!isEdit"/>
      </div>
      <div class="info">
        <label for="phone">電話</label>
        <input type="text" placeholder="請輸入電話" v-model="phone" id="phone" :disabled="!isEdit"/>
      </div>
      <Button 
        btnText="存檔"
        btnColor="#344bb0"
        v-if="isEdit"
      />
    </form>
    <div v-if="!isEdit" class="edit-btn">
      <Button 
        btnText="編輯"
        btnColor="#344bb0"
        @click="isEdit = !isEdit"
      />
    </div>
  </div>
</template>
<script setup>
import Button from './common/_Button.vue';
import Loading from './common/_Loading.vue';
import { auth, db } from '../firebase/init.js';
import { doc, setDoc, getDoc } from 'firebase/firestore';
import { ref } from 'vue';

const address = ref('');
const phone = ref('');
const id = auth.currentUser.uid;
const isLoading = ref(false);
const isEdit = ref(false);


const getData = async () => {
  isLoading.value = true;
  const docRef = doc(db, "members", auth.currentUser.uid);
  const docSnap = await getDoc(docRef);
  
  address.value = docSnap.data().address;
  phone.value = docSnap.data().phone;
  isLoading.value = false;
}

getData();

const submit = async () => {
  const docRef = doc(db, "members", id);
  const payload = {
    userID: id,
    address: address.value,
    phone: phone.value
  }
  isLoading.value = true;
  try{
    await setDoc(docRef, payload, { merge: true});
    alert('存檔成功')
    isEdit.value = false;
    isLoading.value = false;
  }catch(error){
    alert(error.message)
    isLoading.value = false;
  }
}
</script>

<style>
.member-form{
  background-color: #4b6cff;
}
.edit-btn{
  text-align: center;
  padding-top: 20px;
}
</style>