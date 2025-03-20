<template>
  <div
    v-for="exam in exams.data"
    :key="exam.id"
    class="exam-card p-4 bg-white rounded-lg shadow-md hover:shadow-lg transition-shadow"
  >
    <div class="flex items-start gap-3">
      <div class="icon-wrapper mt-1">
        <i class="pi pi-calendar text-blue-500 text-xl"></i>
      </div>
      <div class="exam-details flex-1">
        <h3 class="text-lg font-semibold text-gray-800 mb-2">
          {{ exam.title }}
        </h3>
        <div class="time-info flex items-center text-gray-600">
          <i class="pi pi-clock mr-2"></i>
          <span>{{ exam.date }},{{ exam.timeStart }} » {{ exam.timeEnd }}</span>
        </div>
        <div class="mt-3 flex gap-2">
          <Button
            label="Chi tiết"
            icon="pi pi-info-circle"
            severity="info"
            size="small"
          />
          <Button
            label="Tham gia"
            icon="pi pi-arrow-right"
            severity="success"
            size="small"
            @click="handleTest(exam._id)"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { useRouter } from "vue-router";
import Button from "primevue/button";
import axios from "axios";

const router = useRouter();
const exams = ref([]);
const TOKEN =
  "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjY3YjJmNzc2YjZhNjZkODA0NzU3NzY5ZiIsImlhdCI6MTc0MjM0OTMzOSwiZXhwIjoxNzQyNTIyMTM5fQ.KkZ23byu2LlQOizhWRIJxgsmM6yvLUsVClyjgpDp52M";
const fetchExams = async () => {
  try {
    const response = await axios.get(
      `${import.meta.env.VITE_HOST_URL}/exam/UpcomingExam`,
      {
        headers: {
          Authorization: `Bearer ${TOKEN}`,
        },
      }
    );
    exams.value = response.data;
  } catch (error) {
    console.error("Error fetching exams:", error);
  }
};

onMounted(() => {
  fetchExams();
});

const handleTest = (examId) => {
  if (!examId) {
    console.error("Invalid exam ID");
    return;
  }

  try {
    localStorage.setItem("currentExamId", examId);
    router.push({
      path: "/test",
      query: { examId },
    });
  } catch (error) {
    console.error("Error saving exam ID:", error);
  }
};
</script>

<style scoped>
.exam-card {
  border: 1px solid #e2e8f0;
}

.exam-card:hover {
  border-color: #cbd5e1;
}

.time-info {
  font-size: 0.95rem;
}
</style>
