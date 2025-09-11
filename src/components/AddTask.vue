<script setup>
import { ref } from 'vue';


defineProps({
  msg: String,
})
const nameTodo = ref('')
const descriptionTodo = ref('')
const handleSubmit = () => {
  const todos = JSON.parse(localStorage.getItem('todos') || '[]');
  console.log('Danh sách todos hiện tại:', todos);
  const newTodo = {
    id: Date.now(),
    name: nameTodo.value,
    description: descriptionTodo.value,
    status: 1, // 1: chưa làm, 2: đã làm;3 đang làm; 4: đã hủy
  };
  todos.push(newTodo);
  localStorage.setItem('todos', JSON.stringify(todos));
  nameTodo.value = '';
  descriptionTodo.value = '';
  console.log('Đã lưu todo:', newTodo)
}
</script>

<template>
  <div 
    class="modal fade" 
    id="exampleModal" 
    tabindex="-1" 
    aria-labelledby="exampleModalLabel" 
    aria-hidden="true">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel">Thêm mới todo</h5>
          <button 
            type="button" 
            class="btn-close" 
            data-bs-dismiss="modal" 
            aria-label="Close"
          ></button>
        </div>
        <div class="modal-body">
          <form @submit.prevent="handleSubmit">
            <div class="mb-3">
            <label class="form-label">Tên todo</label>
            <input type="text" v-model="nameTodo" class="form-control" id="name_todo">
            </div>
            <div class="mb-3">
            <label class="form-label">Mô tả</label>
            <textarea class="form-control" id="description_todo" v-model="descriptionTodo"></textarea>
            </div>
            <div class="modal-footer">
          <button 
            type="button" 
            class="btn btn-secondary" 
            data-bs-dismiss="modal"
          > Hủy
          </button>
          <button type="submit" class="btn btn-primary">Thêm mới</button>
        </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>