<template>
  <div class="container">
      <Loading v-if="isLoading"/>
      <!-- <button @click="console.log(auth.currentUser)">測試</button> -->
      <div v-if="isLogin">
        <div class="login-header">
          <p class="state">已登入</p>
          <Button 
            btnText="登出"
            btnColor="red"
            @click="logout"
          />
        </div>
        <MemberForm />
      </div>
      <template v-else>
        <div class="change-btn">
          <Button 
            :btnText="title"
            btnColor="black"
            @click="state === 'signup' ? state = 'login' : state = 'signup'"
          />
        </div>
        <SignUp 
          v-if="state === 'signup'"
          @login="isLogin = true"
          
        />
        <LoginForm 
          v-else
          @login="isLogin = true"  
        />
      </template>
  </div>
</template>

<script setup>
import LoginForm from './components/LoginForm.vue';
import SignUp from './components/SignUp.vue';
import Button from './components/common/_Button.vue';
import MemberForm from './components/MemberForm.vue';
import Loading from './components/common/_Loading.vue';

import { signOut } from 'firebase/auth'
import { auth } from './firebase/init.js';
import { ref, computed, onMounted } from 'vue';

const state = ref('signup');
const isLogin = ref(false);
const isLoading = ref(false);

const title = computed(() => 
  state.value === 'signup' ? '切換登入' : '切換註冊'
)

const logout = () => {
  isLoading.value = true;
  signOut(auth)
    .then(() => {
      isLogin.value = false;
      alert('登出成功')
      isLoading.value = false;
    })
    .catch((error) => {
      alert(error.message)
      isLoading.value = false;
    })
}

onMounted(() => {
  if(auth.currentUser !== null){
    isLogin.value = true;
  }
})
</script>

<style lang="scss">
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  height: 100vh;
  background: #383838;
}
.change-btn{
  margin-bottom: 20px;
}
.login-header{
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 20px;
  padding: 0 20px;
}
.state{
  color: #ffffff;
  font-size: 20px;
  margin: 0;
}
</style>
