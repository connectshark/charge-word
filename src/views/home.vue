<template>
<div class="charge">
  <p class="word">充電人生，充電工作，充電充電充電充電充電充電</p>
  <div class="btns">
    <input type="button" value="充電!!" class="btn" @click="start">
  </div>
</div>
</template>

<script>
import { ref, watch } from 'vue'
export default {
  setup () {
    const progress = ref(100)

    let allowClick = true

    watch(progress, value => {
      if (value <= 0) {
        allowClick = true
        return
      }
      allowClick = false
      setTimeout(() => {
        progress.value = value - 1
        setProgress()
      }, 30)
    })

    const start = () => {
      if (allowClick) {
        if (progress.value === 0) {
          progress.value = 100
        } else {
          --progress.value
        }
      }
    }

    function setProgress () {
      document.querySelector(':root').style.setProperty(`--progress`, progress.value)
    }

    return {
      progress,
      start
    }
  }
}
</script>

<style lang="scss" scoped>
.charge{
  background-color: #000;
  min-height: 100vh;
  display: flex;
  flex-flow: column nowrap;
  align-items: center;
  justify-content: center;
  .word{
    width: 80%;
    max-width: 600px;
    margin: 0 auto;
    color: transparent;
    font-size: 80px;
    background-image: linear-gradient(#fff calc(var(--progress) * 1%), #4cd265 calc(var(--progress) * 1%));
    background-clip: text;
  }
  .btns{
    .btn{
      display: inline-block;
      border: none;
      border-radius: 10px;
      width: 80px;
      height: 30px;
    }
  }
}
</style>