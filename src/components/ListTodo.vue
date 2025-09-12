<script setup>
import { ref } from 'vue';
import EditTodo from './EditTodo.vue';
const listTodo = ref(JSON.parse(localStorage.getItem('todos') || '[]'))

const deleteTodo = (id) => {
  const confirmDelete = confirm('Bạn có chắc chắn muốn xóa ko?')
  if (!confirmDelete) return
  listTodo.value = listTodo.value.filter(todo => todo.id !== id)
  localStorage.setItem('todos', JSON.stringify(listTodo.value))
}

const editTodo = (id) => {
  const modal = new bootstrap.Modal(document.getElementById('editModalTodo'))
  modal.show()
}
</script>

<template>
 <main class="content">
  <table class="table">
  <thead>
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
          <button class="btn btn-sm btn-warning me-2" data-bs-toggle="modal" data-bs-target="#editModalTodo"@click="editTodo(todo.id)">
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
<EditTodo></EditTodo>
</template>

<style scoped>
.content {
  flex: 1;
  padding: 20px;
  box-sizing: border-box;
}
</style>
