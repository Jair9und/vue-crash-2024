<script setup>
import { RouterLink } from 'vue-router';
import { ref, computed } from 'vue';

const props = defineProps({
  job: Object,
})

const showFullDescription = ref(false);

const toggleFullDescription = () => {
  showFullDescription.value = !showFullDescription.value
}

const truncatedDesctiption = computed(() => {
  let description = props.job.description;
  if (!showFullDescription.value) {
    description = description.substring(0, 90) + '...';
  }
  return description;
})
</script>

<template>
  <div class="bg-white rounded-xl shadow-md relative">
    <img src="https://images.unsplash.com/photo-1587691592099-24045742c181?q=80&w=2073&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D" 
      alt="Job Image" 
      class="w-full h-64 object-cover rounded-t-xl" 
    />
    <div class="p-4">
      <div class="mb-6">
        <div class="text-gray-600 my-2">{{ job.type }}</div>
        <h3 class="text-xl font-bold">{{ job.title }}</h3>
      </div>

      <div class="mb-5">
        <div>
          {{ truncatedDesctiption }}
        </div>
        <button @click="toggleFullDescription" class="text-green-500 hover:text-green-600 mb-5">
          {{ showFullDescription ? 'Less' : 'More' }}
        </button>
      </div>

      <h3 class="text-green-500 mb-2">{{ job.salary }}</h3>

      <div class="border border-gray-100 mb-5"></div>

      <div class="flex flex-col lg:flex-row justify-between mb-4">
        <div class="text-orange-700 mb-3">
          <i class="pi pi-map-marker text-orange-700"></i>
          {{ job.location }}
        </div>
        <RouterLink :to="'/jobs/' + job.id"
          class="h-[36px] bg-green-500 hover:bg-green-600 text-white px-4 py-2 rounded-lg text-center text-sm">
          Read More
        </RouterLink>
      </div>
    </div>
  </div>
</template>