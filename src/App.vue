<script setup>
import Home from './components/Home.vue'
import SideBar from './components/SideBar.vue'
import Content from './components/Content.vue'

</script>

<template>
  <Home></Home>
    <div class="wrapper">
      <SideBar></SideBar>
      <Content></Content>
    </div>
</template>

<style scoped>
.wrapper {
  display: flex;
  width: 100%;
  height: 100%;
}
</style>
