<template>
  <button>{{ props.btnText }}</button>
</template>

<script setup>
import { defineProps } from 'vue';
const props = defineProps({
  btnText: {
    type: String,
  },
  btnColor: {
    type: String,
  }
})
</script>

<style>
button{
  padding: 10px;
  border: none;
  border-radius: 5px;
  background: v-bind(btnColor);
  color: rgb(255, 255, 255);
  font-size: 16px;
  cursor: pointer;
}
</style>