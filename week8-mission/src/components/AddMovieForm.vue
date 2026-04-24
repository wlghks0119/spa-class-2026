<script setup>
import { ref } from 'vue';

const emit = defineEmits(['add-movie']);

const title = ref('');
const rating = ref('');

const submitForm = () => {
  // 방어 로직: 필수값 체크
  if (!title.value.trim() || !rating.value) {
    alert('영화 제목과 평점을 모두 입력해주세요!');
    return;
  }

  // 부모에게 데이터 전달
  emit('add-movie', {
    title: title.value,
    rating: Number(rating.value)
  });

  // 입력창 초기화
  title.value = '';
  rating.value = '';
};
</script>

<template>
  <div class="form-container">
    <h3>새 영화 등록</h3>
    <div class="input-group">
      <input v-model="title" type="text" placeholder="영화 제목 입력" class="input-field" />
      <input v-model="rating" type="number" step="0.1" min="0" max="10" placeholder="평점 (0~10)" class="input-field" />
      <button @click="submitForm" class="add-btn">등록</button>
    </div>
  </div>
</template>

<style scoped>
.form-container {
  background: white;
  padding: 20px;
  border-radius: 12px;
  box-shadow: 0 4px 6px rgba(0,0,0,0.05);
  margin-bottom: 30px;
  border: 1px solid #e0e0e0;
}

h3 { margin-top: 0; color: #2c3e50; }

.input-group {
  display: flex;
  gap: 10px;
}

.input-field {
  flex: 1;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 6px;
}

.add-btn {
  padding: 10px 25px;
  background-color: #2ecc71;
  color: white;
  border: none;
  border-radius: 6px;
  font-weight: bold;
  cursor: pointer;
  transition: background 0.2s;
}

.add-btn:hover { background-color: #27ae60; }
</style>