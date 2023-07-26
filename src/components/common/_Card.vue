<template>
  <div class="card form-Box">
    <h2 class="title">{{ props.title }}</h2>
    <form @submit.prevent="props.action(email, password)">
      <div class="info">
        <label for="mail">信箱</label>
        <input type="text" placeholder="請輸入電子信箱" v-model="email" id="mail"/>
      </div>
      <div class="info">
        <label for="loginPassword">密碼</label>
        <input type="password" placeholder="請輸入密碼" v-model="password" id="loginPassword"/>
      </div>
      <Button 
        :btnText="props.btnText"
        :btnColor="props.btnColor"
      />
    </form>
  </div>
</template>

<script setup>
import Button from './_Button.vue';
import { ref, defineProps } from 'vue';

const props = defineProps({
  title: {
    type: String,
  },
  action: {
    type: Function,
  },
  bgColor: {
    type: String,
  },
  btnColor: {
    type: String,
  },
  btnText: {
    type: String,
  }
})

const email = ref('');
const password = ref('');
</script>

<style>
.form-Box{
  width: 400px;
  padding: 30px;
  border-radius: 30px;
  box-shadow: 0 0 20px 5px #ffffff;
}
.card{
  background: v-bind(bgColor);
}
form{
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
  gap: 20px;
}
.title{
  color: rgb(250, 250, 250);
  text-align: center;
  margin-top: 0;
  font-size: 30px;
}
.info{
  display: flex;
  width: 100%;
  align-items: center;
  gap: 10px;
  color: rgb(250, 250, 250);
}
input{
  flex-grow: 1;
  padding: 10px;
  border: none;
  border-radius: 5px;
}
</style>