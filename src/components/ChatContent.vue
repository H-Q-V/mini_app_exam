<template>
  <div
    v-if="exams"
    class="flex mx-5 justify-around py-2 mb-2"
    style="border-bottom: 1px solid #ccc"
  >
    <div class="flex flex-col justify-center items-start">
      <div class="flex justify-center items-center gap-2">
        <p>Môn thi:</p>
        <p>{{ exams.subject }}</p>
      </div>
      <div class="flex justify-center items-center gap-2">
        <p>Thời gian:</p>
        <p>{{ exams.duration }} phút</p>
      </div>
    </div>
    <div>
      <div class="flex justify-center items-center gap-2">
        <p>Kì thi:</p>
        <p>{{ exams.description }}</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";

const exams = ref(null);
const checked = ref(false);
const TOKEN =
  "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjY3YjJmNzc2YjZhNjZkODA0NzU3NzY5ZiIsImlhdCI6MTc0MjM0OTMzOSwiZXhwIjoxNzQyNTIyMTM5fQ.KkZ23byu2LlQOizhWRIJxgsmM6yvLUsVClyjgpDp52M";
const fetchExam = async () => {
  try {
    const examId = localStorage.getItem("currentExamId");
    const response = await axios.get(
      `${import.meta.env.VITE_HOST_URL}/exam/getOne/${examId}`,
      {
        headers: {
          Authorization: `Bearer ${TOKEN}`,
        },
      }
    );
    exams.value = response.data.data;
    if (exams.value?.duration) {
      localStorage.setItem("examDuration", exams.value.duration);
    }
  } catch (error) {
    console.error("Error fetching exams:", error);
  }
};

onMounted(() => {
  fetchExam();
});
</script>
