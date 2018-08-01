<template>
  <div>
    about组件
    <p>{{msg}}</p>
    <input type="text">
  </div>
</template>

<script>
  export default {
    // 声明接收属性
    props: ['msg']
  }
</script>

<style>

</style>