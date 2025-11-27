<script setup>
import { ref } from 'vue'
const todoList = ref([]) 
const inputValue = ref('')
const handleAdd = () => {
  if (!inputValue.value.trim()) return
  todoList.value.push({
    id: Date.now(), 
    content: inputValue.value
  })
  inputValue.value = '' 
}
const handleDelete = (id) => {
  todoList.value = todoList.value.filter(item => item.id !== id)
}
const handleClearAll = () => {
  if (todoList.value.length === 0) return;

  if (confirm('是否要清空所有待办事项')) {
    todoList.value = []
  }
}
</script>

<template>
  <div class="app-container">
    <div class="todo-box">
      <h1 class="title">本周待办事项</h1>

      <div class="list-container">
        <div v-for="item in todoList" :key="item.id" class="list-item">
          <span class="item-text">{{ item.content }}</span>
          <button class="btn-delete" @click="handleDelete(item.id)">删除</button>
        </div>
        
        <div v-if="todoList.length === 0" class="empty-tip">
          暂无待办事项
        </div>
      </div>

      <div class="input-group">
        <input 
          v-model="inputValue" 
          @keyup.enter="handleAdd"
          type="text" 
          placeholder="请输入待办事项..." 
          class="input-field"
        />
        <button class="btn-add" @click="handleAdd">添加</button>
      </div>

      <div class="footer">
        <button class="btn-clear" @click="handleClearAll">清空所有</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.app-container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: flex-start;
  padding-top: 50px;
  background-color: #ffffff;
  font-family: "PingFang SC", "Microsoft YaHei", sans-serif;
}

.todo-box {
  width: 500px;
  background-color: #f5f5f5;
  padding: 30px;
  border-radius: 8px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.title {
  text-align: center;
  color: #333;
  margin-bottom: 30px;
  font-size: 24px;
  font-weight: bold;
}

.list-container {
  margin-bottom: 20px;
  min-height: 50px; /* 保持一点高度，防止没有数据时太扁 */
}

.list-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: white;
  padding: 15px 20px;
  margin-bottom: 10px;
  border-radius: 6px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.02);
}

.item-text {
  font-size: 16px;
  color: #333;
}

.input-group {
  display: flex;
  gap: 10px;
  margin-bottom: 30px;
}

.input-field {
  flex: 1;
  padding: 12px;
  border: 2px solid #ddd;
  border-radius: 6px;
  font-size: 14px;
  outline: none;
  transition: border-color 0.3s;
}

.input-field:focus {
  border-color: #007bff;
}

button {
  cursor: pointer;
  border: none;
  border-radius: 4px;
  font-size: 14px;
  transition: opacity 0.2s;
}

button:hover {
  opacity: 0.8;
}

.btn-delete {
  background-color: #dc3545;
  color: white;
  padding: 8px 16px;
}

.btn-add {
  background-color: #007bff;
  color: white;
  padding: 0 24px;
  font-size: 16px;
}

.footer {
  display: flex;
  justify-content: center;
}

.btn-clear {
  background-color: #6c757d;
  color: white;
  padding: 10px 30px;
}

.empty-tip {
  text-align: center;
  color: #999;
  padding: 20px;
  border: 2px dashed #eee; 
  border-radius: 6px;
}
</style>
