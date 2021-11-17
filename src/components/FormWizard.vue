<template>
  <form @submit="onSubmit">
    <h2>{{ ( '00' + (currentStepIdx + 1) ).slice(-2) }} / {{ ( '00' + stepCounter ).slice(-2) }}</h2>
    <div class="form-group">
      <slot />
    </div>
    <div class="button-group">
      <button class="prev-button" v-if="hasPrevious" type="button" @click="goToPrev">まえの質問へ</button>
      <button class="next-button" type="submit">{{ isLastStep ? "計算結果へ" : "つぎの質問へ" }}</button>
    </div>
  </form>
</template>

<script>
import { useForm } from "vee-validate";
import { ref, computed, provide } from "vue";

export default {
  name: "FormWizard",
  emits: ["next", "submit"],
  props: {
    validationSchema: {
      type: Array,
      required: true,
    },
  },
  setup(props, { emit }) {
    const formData = ref({});
    const currentStepIdx = ref(0);
    const stepCounter = ref(0);
    provide("STEP_COUNTER", stepCounter);
    provide("CURRENT_STEP_INDEX", currentStepIdx);

    const isLastStep = computed(() => currentStepIdx.value === stepCounter.value - 1)

    const hasPrevious = computed(() => currentStepIdx.value > 0)

    const currentSchema = computed(() => props.validationSchema[currentStepIdx.value])

    // useFormでバリデーションスキーマを定義する
    const { resetForm, handleSubmit } = useForm({
      validationSchema: currentSchema,
    })

    // handleSubmitでバリデーションチェックが終わってから処理を行う。
    const onSubmit = handleSubmit((values) => {
      formData.value = {
        ...formData.value,
        ...values,
      }

      // すでに入力された値を引数として初期値設定を行うことで、
      // 「まえの質問へ」を選択しても、値がセットされた状態になる。
      resetForm({
        values: {
          ...formData.value,
        },
      })

      if (!isLastStep.value) {
        currentStepIdx.value++
        return
      }

      emit("submit", formData.value)
    });

    const goToPrev = () => {
      if (currentStepIdx.value === 0) return

      currentStepIdx.value--
      resetForm({
        values: {
          ...formData.value,
        },
      })
    }

    return {
      currentStepIdx,
      stepCounter,
      onSubmit,
      hasPrevious,
      isLastStep,
      goToPrev
    };
  },
};
</script>

<style scoped>
.form-group {
  display: flex;
  justify-content: center;
  align-items: center;
}

.button-group {
  display: flex;
  justify-content: space-around;
  margin-top: 10px;
}

.next-button {
  display: block;
  width: 160px;
  padding: 0.8em;
  text-align: center;
  text-decoration: none;
  color: #fff;
  background: #117766;
  border:1px solid #fff;
  border-radius: 20px;
  overflow: hidden;
  box-shadow: 0px 4px rgba(0, 0, 0, 0.1);
}

.prev-button {
  display: block;
  width: 160px;
  padding: 0.8em;
  text-align: center;
  text-decoration: none;
  color: #000;
  background: #DFEEE5;
  border:1px solid #fff;
  border-radius: 20px;
  overflow: hidden;
  box-shadow: 0px 4px rgba(0, 0, 0, 0.1);
}

</style>
