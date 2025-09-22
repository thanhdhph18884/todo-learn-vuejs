<script setup>
import { ref, computed, onMounted} from 'vue';
import EditTodo from './EditTodo.vue';
import AddTask from './AddTask.vue';
import DataTable from "primevue/datatable";
import Column from "primevue/column"; 
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
const columns = [
    { field: 'name', header: 'Name' },
    { field: 'description', header: 'Description' },
    { field: 'dateData', header: 'Date' },
    { field: 'status', header: 'Trạng thái' },
];
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
<div class="card">
  <DataTable :value="listTodo" tableStyle="min-width:50rem">
    <Column header="STT">
      <template #body="s">{{ s.index + 1 }}</template>
    </Column>
    <Column v-for="c in columns" :key="c.field" :field="c.field" :header="c.header" />
  </DataTable>
</div>
<EditTodo :todo="currentTodo" @update="updateTodo"></EditTodo>
</template>