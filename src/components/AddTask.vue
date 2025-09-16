<script setup>
import { ref } from 'vue';
const emitNotify = defineEmits(['todo_added'])
const today = ref(new Date())
const STATUS = {
  PENDING: "pending",
  DONE: "done",
  IN_PROGRESS: "in-progress",
  CANCELED: "canceled",
}
const nameTodo = ref('')
const descriptionTodo = ref('')
const nameError = ref('')
const descriptionError = ref('')
const dateTodo = ref('')
const dateTodoError = ref('')
function addTodo() {
  nameError.value = ''
  descriptionError.value = ''
  if (!nameTodo.value.trim()) {
    nameError.value = 'Tên todo không được để trống'
  }
  if (!descriptionTodo.value.trim()) {
    descriptionError.value = 'Mô tả không được để trống'
  }
  if (!dateTodo.value.trim()) {
    dateTodoError.value = 'Lịch không được để trống'
  }
  if (nameError.value || descriptionError.value || dateTodoError.value) return

  const todos = JSON.parse(localStorage.getItem('todos') || '[]')
  const dateData = dateTodo.value ? dateTodo.value : today.value.toISOString().split('T')[0]

  todos.push({
    id: Date.now(),
    name: nameTodo.value,
    description: descriptionTodo.value,
    status: STATUS.PENDING,
    dateData : dateData
  })
  localStorage.setItem('todos', JSON.stringify(todos))
  window.location.reload()
}
</script>
<template>
  <div 
    class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
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
          <form @submit.prevent="addTodo">
            <div class="mb-3">
            <label class="form-label">Tên todo</label>
            <input type="text" placeholder="nhập tên" v-model="nameTodo" class="form-control" id="name_todo">
            <div class="text-danger" v-if="nameError">{{ nameError }}</div>
            </div>
            <div class="mb-3">
            <label class="form-label">Mô tả</label>
            <textarea class="form-control" placeholder="nhập mô tả" id="description_todo" v-model="descriptionTodo"></textarea>
            <div class="text-danger" v-if="descriptionError">{{ descriptionError }}</div>
            </div>
            <div class="mb-3">
            <label class="form-label">Lịch</label>
            <input type="date" placeholder="nhập tên" v-model="dateTodo" class="form-control" id="date_todo">
            <div class="text-danger" v-if="dateTodoError">{{ dateTodoError }}</div>
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