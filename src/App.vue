<template>
  <div class="container">
      <button @click="console.log(auth.currentUser)">dfddsfdsfd</button>
      <div v-if="isLogin">
        <p>已登入</p>
        <Button 
          btnText="登出"
          btnColor="red"
          @click="logout"
        />
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
import { signOut } from 'firebase/auth'
import { auth } from './firebase/init.js';
import { ref, computed } from 'vue';

const state = ref('signup');
const isLogin = ref(false);

const title = computed(() => 
  state.value === 'signup' ? '切換登入' : '切換註冊'
)

const logout = () => {
  signOut(auth)
    .then(() => {
      isLogin.value = false;
      alert('登出成功')
    })
    .catch((error) => {
      alert(error.message)
    })
}
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
</style>
