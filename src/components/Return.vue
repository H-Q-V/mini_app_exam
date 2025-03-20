<template>
  <div
    class="bg-[#0f5c56] text-white px-4 py-4 flex justify-between items-center fixed top-0 left-0 right-0 max-w-md mx-auto z-50"
  >
    <div class="mt-10 flex items-center gap-3">
      <div class="flex flex-wrap gap-4 justify-center">
        <!-- <Button label="Trở về" icon="pi pi-arrow-left" @click="handleReturn" /> -->
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-6 w-6 text-white-800"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
          @click="handleReturn"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M15 19l-7-7 7-7"
          />
        </svg>
        <!-- <span class="text-lg font-medium">Cá nhân</span> -->
      </div>
    </div>
  </div>
</template>

<script setup>
import { useRouter } from "vue-router";
import Button from "primevue/button";

const router = useRouter();

const handleReturn = () => {
  router.push("/home");
};
</script>
<!-- Header with back button -->
<!-- <div class="flex items-center mb-4">
  <svg
    xmlns="http://www.w3.org/2000/svg"
    class="h-6 w-6 text-gray-800"
    fill="none"
    viewBox="0 0 24 24"
    stroke="currentColor"
  >
    <path
      stroke-linecap="round"
      stroke-linejoin="round"
      stroke-width="2"
      d="M15 19l-7-7 7-7"
    />
  </svg>
  <span class="ml-4 text-lg font-medium">Cá nhân</span>
</div> -->
