<template>
  <div class="loading-container">
    <div class="loading">
      <span></span>
    </div>
  </div>
</template>

<script setup>
</script>

<style>
.loading-container{
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background: rgba(0, 0, 0, 0.788);
  display: flex;
  justify-content: center;
  align-items: center;
}
.loading{
  width: 200px;
  height: 200px;
  box-sizing: border-box;
  border-radius: 50%;
  border-top: 10px solid #63A69F;
  position: relative;    
  animation: a1 2s linear infinite;
}
.loading::before,.loading::after{
  content: "";
  width: 200px;
  height: 200px;
  position: absolute;
  left: 0;
  top: -10px;
  box-sizing: border-box;
  border-radius: 50%;
}
.loading::before{
  border-top: 10px solid #F2E1AC;
  transform: rotate(120deg);
}
.loading::after{   
  border-top: 10px solid #F2836B;
  transform: rotate(240deg);
}
.loading span{
  position: absolute;
  width: 200px;
  height: 200px;
  line-height: 200px;
  text-align: center;
  color: #fff;
  animation: a2 2s linear infinite;
}
@keyframes a1{
  to{
    transform: rotate(360deg);
  }
}
@keyframes a2{
  to{
    transform: rotate(-360deg);
  }
}
</style>