<script setup>
import { ref } from 'vue';
import EditTodo from './EditTodo.vue';
const listTodo = ref(JSON.parse(localStorage.getItem('todos') || '[]'))
const currentTodo  = ref(null);

function deleteTodo(id) {
  const confirmDelete = confirm('Bạn có chắc chắn muốn xóa ko?')
  if (!confirmDelete) return
  listTodo.value = listTodo.value.filter(todo => todo.id !== id)
  localStorage.setItem('todos', JSON.stringify(listTodo.value))
}

function editTodo(todo) {
  console.log('vào đây')
  currentTodo.value = { ...todo }
  let modal = new bootstrap.Modal(document.getElementById('editModalTodo'))
  modal.show()
}
function updateTodo(updatedTodo) {
  let index = listTodo.value.findIndex(t => t.id == updatedTodo.id)
  if(index !== -1){
    listTodo.value[index] = updatedTodo
    localStorage.setItem('todos', JSON.stringify(listTodo.value))
  }
}
</script>

<template>
 <main class="content">
  <table class="table table-bordered">
  <thead class="table-secondary">
    <tr>
      <th scope="col">STT</th>
      <th scope="col">Tên</th>
      <th scope="col">Mô tả</th>
      <th scope="col">Trạng thái</th>
      <th scope="col">Hành động</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(todo,index) in listTodo" :key="todo.id">
      <th scope="row">{{ index + 1 }}</th>
      <td>{{ todo.name }}</td>
      <td>{{ todo.description }}</td>
      <td>{{ todo.status }}</td>   
      <td>
          <button class="btn btn-sm btn-warning me-2" data-bs-toggle="modal" data-bs-target="#editModalTodo" @click="editTodo(todo)">
              <i class="las la-edit la-2x"></i>
            </button>
          <button class="btn btn-sm btn-danger" @click="deleteTodo(todo.id)">
            <i class="las la-trash-alt la-2x"></i>
          </button>
        </td>  
    </tr>
  </tbody>
</table> 
</main>
<EditTodo :todo="currentTodo" @update="updateTodo"></EditTodo>
</template>

<style scoped>
.content {
  flex: 1;
  padding: 20px;
  box-sizing: border-box;
}
</style>
