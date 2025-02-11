<template >
  <div class="w-full h-screen bg-neutral-50 flex flex-col justify-center items-center">
    <accordion></accordion>
  </div>
</template>
<script>
import accordion from './components/accordionComponent.vue'
import { ref } from "vue";
export default {
  components : {
    accordion
  },
  setup() {
    

    return {
      
    }
  }
}
</script>
