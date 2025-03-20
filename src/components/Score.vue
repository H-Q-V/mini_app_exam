<template>
  <div class="score-container">
    <h2>Kết quả bài làm của bạn</h2>
    <div class="score-details">
      <p>Điểm số: {{ score }}/10</p>
      <p>Số câu đúng: {{ correctAnswers }}/{{ totalQuestions }}</p>
      <p>Thời gian làm bài: {{ timeTaken }} phút</p>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const score = ref(0);
const correctAnswers = ref(0);
const totalQuestions = ref(10);
const timeTaken = ref(0);
</script>

<style scoped>
.score-container {
  padding: 1rem;
  text-align: center;
}

.score-details {
  margin-top: 1rem;
}

.score-details p {
  margin: 0.5rem 0;
}
</style>
