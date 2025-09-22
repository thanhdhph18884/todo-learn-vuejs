<script setup>
import { ref } from 'vue';
const filterStatus = defineModel('filterStatus', { type: String, default: 'all' })


defineProps({
  msg: String,
})

const count = ref(30)
</script>

<template>
  <aside class="sidebar">
    <div class="info_name">
      <h5 style="white-space: nowrap">Đinh Hữu Thành<i class="las la-angle-down la-xs"></i></h5>
      <button type="button" class="btn btn-light position-relative button_bell">
        <i class="las la-bell icon_bell"></i>
        <span class="position-absolute top-0 start-100 translate-middle badge rounded-pill bg-danger">5</span>
      </button>
    </div>
    <div>
      <ul class="menu">
      <li data-bs-toggle="modal" data-bs-target="#exampleModal" class="add-task-item">  <span class="icon-circle"><i class="las la-plus"></i></span>Add task</li>
      <li @click="filterStatus = 'all'"><i class="las la-list-alt"></i>All</li>
      <li @click="filterStatus = 'pending'"><i class="las la-calendar-day"></i>Pending</li>
      <li @click="filterStatus = 'in-progress'"><i class="las la-times-circle"></i>In-Progress</li>
      <li @click="filterStatus = 'done'"><i class="las la-check"></i>Done</li>
    </ul>
    </div>
  </aside>
</template>

<style scoped>
.sidebar {
  width: 240px;
  background: #fafafa;
  border-right: 1px solid #ddd;
  padding: 15px;
  box-sizing: border-box;
}

.menu {
  list-style: none;
  padding: 0;
  margin: 0;
}

.menu li {
  display: flex;
  align-items: center;
  gap: 10px;
  font-size: 16px;
  padding: 8px 10px;
  margin: 4px 0;
  border-radius: 6px;
  cursor: pointer;
  color: #333;
}

.menu li i {
  font-size: 20px;
}

.menu li:hover {
  background: #eee;
}

.active {
  background: #fdecea;
  color: #d1453b;
  font-weight: bold;
}

.project-title {
  margin-top: 20px;
  font-size: 14px;
  color: #555;
}
.info_name {
  margin-bottom: 30px;
  display: flex;
  gap: 20px;
}

.button_bell {
  background-color: #f5e3e3;
  padding: 5px;
  margin-top: -5px;
}
.add-task-item {
  display: flex;
  align-items: center;
  gap: 8px;
  cursor: pointer;

  .icon-circle {
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #d1453b;
    color: #fff;
    border-radius: 50%;
    width: 28px;
    height: 28px;

    i {
      font-size: 16px;
      line-height: 1;
    }
  }
}
</style>
