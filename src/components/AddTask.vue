<script setup>
import { ref } from 'vue';


defineProps({
  msg: String,
})

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
          <form>
            <div class="mb-3">
            <label class="form-label">Tên todo</label>
            <input type="text" name="name_todo" class="form-control" id="name_todo">
            </div>
            <div class="mb-3">
            <label class="form-label">Mô tả</label>
            <textarea class="form-control" id="description_todo" name="description_todo"></textarea>
            </div>
          </form>
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
      </div>
    </div>
  </div>
</template>