<script setup>
import { ref } from 'vue';


defineProps({
  msg: String,
})

const count = ref(30)
</script>

<template>
 <main class="content">
        <h1>Today</h1>
        <p>Nội dung sẽ hiển thị ở đây...</p>
      </main>
</template>

<style scoped>
.content {
  flex: 1;
  padding: 20px;
  box-sizing: border-box;
}
</style>
