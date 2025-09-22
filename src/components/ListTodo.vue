<script setup>
import { ref } from 'vue';
import EditTodo from './EditTodo.vue';
import AddTask from './AddTask.vue';
import DataTable from "primevue/datatable";
import Column from "primevue/column"; 
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
const columns = [
    { field: 'STT', header: 'STT' },
    { field: 'name', header: 'Name' },
    { field: 'description', header: 'Description' },
    { field: 'date', header: 'Date' },
    { field: 'status', header: 'Trạng thái' },
];

</script>

<template>
 <div class="card">
        <DataTable :value="listTodo" tableStyle="min-width: 50rem">
            <Column v-for="col of columns" :key="col.field" :field="col.field" :header="col.header"></Column>
        </DataTable>
    </div>
<EditTodo></EditTodo>
</template>

<style scoped>
.content {
  flex: 1;
  padding: 20px;
  box-sizing: border-box;
}
</style>