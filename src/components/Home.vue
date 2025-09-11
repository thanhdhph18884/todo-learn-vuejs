<script setup>
import { ref } from 'vue';
import AddTask from './AddTask.vue';



defineProps({
  msg: String,
})

const count = ref(30)
</script>

<template>
<AddTask></AddTask>
</template>

<style scoped>

</style>
