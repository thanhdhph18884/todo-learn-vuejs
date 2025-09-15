<script setup>
import { ref, watch } from 'vue';
import { Modal } from 'bootstrap'

const props = defineProps({ todo: Object })
const emit = defineEmits(['update'])
const nameEdit = ref('')
const nameError = ref('')
const descriptionError = ref('')
const descriptionEdit = ref('')
const statusEdit = ref('')

watch(() => props.todo, (newVal) => {
  if (newVal) {
    nameEdit.value = newVal.name
    descriptionEdit.value = newVal.description
    statusEdit.value = newVal.status
  }
}, { immediate: true })
function updateTodo() {
  nameError.value = ''
  descriptionError.value = ''
  if (!nameEdit.value.trim()) {
    nameError.value = 'Tên todo không được để trống'
  }
  if (!descriptionEdit.value.trim()) {
    descriptionError.value = 'Mô tả không được để trống'
  }
  if (nameError.value || descriptionError.value) return
 emit('update', {
  id: props.todo?.id,
  name: nameEdit.value,
  description: descriptionEdit.value,
  status: statusEdit.value
  })
  window.location.reload()
}
</script>

<template>
    <div class="modal fade" id="editModalTodo" tabindex="-1">
    <div class="modal-dialog">
      <div class="modal-content">
        <form @submit.prevent="updateTodo">
          <div class="modal-header">
            <h5 class="modal-title">Sửa Todo</h5>
            <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
          </div>
          <div class="modal-body">
            <div class="mb-3">
              <label class="form-label">Tên</label>
              <input v-model="nameEdit" placeholder="Nhập tên" type="text" class="form-control" />
              <div class="text-danger" v-if="nameError">{{ nameError }}</div>
            </div>
            <div class="mb-3">
              <label class="form-label">Mô tả</label>
              <textarea v-model="descriptionEdit" placeholder="Nhập mô tả" class="form-control"></textarea>
              <div class="text-danger" v-if="descriptionError">{{ descriptionError }}</div>
            </div>
            <div class="mb-3">
              <label class="form-label">Trạng thái</label>
              <select v-model="statusEdit" class="form-select">
                <option value="pending">Pending</option>
                <option value="in-progress">In-Progress</option>
                <option value="done">Done</option>
              </select>
            </div>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Hủy</button>
            <button type="submit" class="btn btn-primary">Cập nhật</button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>
