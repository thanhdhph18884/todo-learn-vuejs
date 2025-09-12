<script setup>
import { ref } from 'vue';

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
              <input v-model="nameEdit" type="text" class="form-control" />
            </div>
            <div class="mb-3">
              <label class="form-label">Mô tả</label>
              <textarea v-model="descriptionEdit" class="form-control"></textarea>
            </div>
            <div class="mb-3">
              <label class="form-label">Trạng thái</label>
              <select v-model="statusEdit" class="form-select">
                <option value="pending">Chưa làm</option>
                <option value="in-progress">Đang làm</option>
                <option value="done">Hoàn thành</option>
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
