<script setup>
import { ref, computed} from 'vue';
import EditTodo from './EditTodo.vue';
const listTodo = ref(JSON.parse(localStorage.getItem('todos') || '[]'))
const currentTodo  = ref(null);
const props = defineProps({
  filterStatus: { type: String }
})
const filteredTodos = computed(() => {
  if (props.filterStatus === 'all') return listTodo.value
  return listTodo.value.filter(todo => todo.status === props.filterStatus)
})
function deleteTodo(id) {
  const confirmDelete = confirm('Bạn có chắc chắn muốn xóa ko?')
  if (!confirmDelete) return
  listTodo.value = listTodo.value.filter(todo => todo.id !== id)
  localStorage.setItem('todos', JSON.stringify(listTodo.value))
}

function editTodo(todo) {
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
function statusClass(status) {
  switch (status) {
    case 'pending':
      return 'status-pending'
    case 'in-progress':
      return 'status-inprogress'
    case 'done':
      return 'status-done'
    default:
      return ''
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
    <tr v-for="(todo,index) in filteredTodos" :key="todo.id">
      <th scope="row">{{ index + 1 }}</th>
      <td>{{ todo.name }}</td>
      <td>{{ todo.description }}</td>
      <td :class="statusClass(todo.status)">
      {{ todo.status }}
      </td>

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
.status-pending {
  color: #d1453b;
  font-weight: bold;
}

.status-inprogress {
  color: #007bff; 
  font-weight: bold;
}

.status-done {
  color: #28a745;
  font-weight: bold;
}

</style>
