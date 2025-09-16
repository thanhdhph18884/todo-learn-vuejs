<script setup>
import { ref } from 'vue'

import Home from './components/Home.vue'
import SideBar from './components/SideBar.vue'
import ListTodo from './components/ListTodo.vue'

const filterStatus = ref('pending')

</script>

<template>
  <Home></Home>
    <div class="wrapper">
      <SideBar v-model:filterStatus="filterStatus" />
      <ListTodo :filter-status="filterStatus" />
    </div>
</template>

<style scoped>
.wrapper {
  display: flex;
  width: 100%;
  height: 100%;
}
</style>
