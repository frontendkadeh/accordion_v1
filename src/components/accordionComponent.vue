<template>
  <div class="w-3xl h-[550px] p-10">
    <div class="w-2xl space-y-2">
      <div v-for="(item, index) in accordionList" :key="index" class="border-2 border-gray-400 rounded-sm   ">
        
        <!-- عنوان آکاردئون -->
        <button 
          @click="toggleAccordion(index)"
          class="w-full text-left flex justify-between font-irsans  text-lg   items-center px-6 py-4 bg-gray-50 hover: text-slate-600 transition duration-300">
          {{ item.title }}
          <span :class="iconClass(index)">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
            <path stroke-linecap="round" stroke-linejoin="round" d="m19.5 8.25-7.5 7.5-7.5-7.5" />
            </svg>

          </span>
        </button>
  
        <!-- محتوای آکاردئون -->
        <div :class="contentClass(index)">
          <p class="py-4 pr-4 text-slate-700 text-md font-irsansLight flex items-center">{{ item.answer }}</p>
        </div>
  
      </div>
    </div>
  </div>
</template>
  
<script>
import { ref, computed } from "vue";

export default {
  setup() {
    const activeIndexes = ref(new Set()); // مدیریت وضعیت باز بودن هر آکاردئون
    const accordionList = [
      { title: 'سوال یک', answer: 'جواب یک' },
      { title: 'سوال دو', answer: 'جواب دو' },
      { title: 'سوال سه', answer: 'جواب سه' },
      { title: 'سوال چهارم', answer: 'جواب چهارم' }
    ];

    // تابع باز و بسته کردن آکاردئون
    const toggleAccordion = (index) => {
      if (activeIndexes.value.has(index)) {
        activeIndexes.value.delete(index);
      } else {
        activeIndexes.value.add(index);
      }
      activeIndexes.value = new Set(activeIndexes.value); // برای بازنشانی ری‌اکتیویتی Vue
    };

    // کلاس آیکون چرخشی برای باز و بسته شدن
    const iconClass = computed(() => (index) =>
      activeIndexes.value.has(index) ? "rotate-180 transition-transform duration-300 text-gray-500" : "rotate-0 transition-transform duration-300 text-gray-500"
    );

    // کلاس نمایش محتوای آکاردئون با انیمیشن ارتفاع
    const contentClass = computed(() => (index) =>
      `overflow-hidden transition-all duration-500 ease-in-out px-6 ${
        activeIndexes.value.has(index) ? "max-h-40 opacity-100 bg-slate-50" : "max-h-0 opacity-0"
      }`
    );

    return {
      activeIndexes,
      toggleAccordion,
      accordionList,
      iconClass,
      contentClass
    };
  }
};
</script>
