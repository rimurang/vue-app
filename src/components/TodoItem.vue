<template>
  <li class="item">
    <span>{{ item }}</span>
    <button class="delete" @click="$emit('remove')">삭제</button>
  </li>
</template>

<script setup>
defineProps({
  item: String,
});
// defineProps로 부모에서 item을 전달받음
// $emit('remove')로 부모에게 삭제해줘! 신호 보냄
</script>

<style scoped>
.item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #f9f9f9;
  border: 1px solid #ddd;
  padding: 8px 12px;
  margin-bottom: 8px;
  border-radius: 6px;
}

.delete {
  background: #ff5c5c;
  color: white;
  border: none;
  padding: 4px 8px;
  border-radius: 4px;
  cursor: pointer;
}

.delete:hover {
  background: #e04848;
}
</style>
