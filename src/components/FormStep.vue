<template>
  <div v-if="shouldShow">
    <slot />
  </div>
</template>

<script>
import { computed, inject } from "vue";
export default {
  setup() {
    const currentIdx = inject("STEP_COUNTER").value++
    const formStepIdx = inject("CURRENT_STEP_INDEX")
    const shouldShow = computed(() => currentIdx === formStepIdx.value)

    return {
      shouldShow,
    }
  },
}
</script>
