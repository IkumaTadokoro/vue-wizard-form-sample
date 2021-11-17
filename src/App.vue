<template>
  <div class="container">
    <h1>quitcost_sample</h1>

    <FormWizard :validation-schema="validationSchema" @submit="onSubmit">
      <FormStep>
        <h2>退職予定月を教えてください</h2>
        <Field name="retirementMonth" type="date" />
        <ErrorMessage name="retirementMonth" />
      </FormStep>

      <FormStep>
        <h2>転職予定月を教えてください</h2>
        <Field name="careerChangeMonth" type="date" />
        <ErrorMessage name="careerChangeMonth" />
      </FormStep>

      <FormStep>
        <h2>年齢を教えてください</h2>
        <Field name="age" type="text" />
        <ErrorMessage name="age" />
      </FormStep>

      <FormStep>
        <h2>お住まいの地域の郵便番号を教えてください</h2>
        <Field name="postalCode" type="text" />
        <ErrorMessage name="postalCode" />
      </FormStep>

      <FormStep>
        <h2>昨年度（2020年1月1日~2020年12月31日）の 「所得」を教えてください</h2>
        <Field name="income" type="text" placeholder="500000円"/>
        <ErrorMessage name="income" />
      </FormStep>

      <FormStep>
        <h2>昨年度（2020年1月1日~2020年12月31日）の 「住民税の総額」を教えてください</h2>
        <Field name="residentTax" type="text" placeholder="500000円"/>
        <ErrorMessage name="residentTax" />
      </FormStep>

      <FormStep>
        <h2>今年度（2021年1月1日~2021年12月31日）の 「予定所得」を教えてください</h2>
        <Field name="scheduledIncome" type="text" placeholder="500000円"/>
        <ErrorMessage name="scheduledIncome" />
      </FormStep>

      <FormStep>
        <h2>今年度（2021年1月1日~2021年12月31日）の 「予定社会保険料」を教えてください</h2>
        <Field name="scheduledInsurance" type="text" placeholder="500000円"/>
        <ErrorMessage name="scheduledInsurance" />
      </FormStep>
    </FormWizard>
  </div>
</template>

<script>
import { Field, ErrorMessage } from "vee-validate";
import * as yup from "yup";
import FormWizard from "@/components/FormWizard.vue";
import FormStep from "@/components/FormStep.vue";

export default {
  name: "App",
  components: {
    FormWizard,
    FormStep,
    Field,
    ErrorMessage,
  },
  setup() {
    const validationSchema = [
      yup.object({
        retirementMonth: yup.date().required(),
      }),
      yup.object({
        careerChangeMonth: yup.date().required(),
      }),
      yup.object({
        age: yup.number().required(),
      }),
      yup.object({
        postalCode: yup.string().matches(/^[0-9]{7}$/).required(),
      }),
      yup.object({
        income: yup.number().required(),
      }),
      yup.object({
        residentTax: yup.number().required(),
      }),
      yup.object({
        scheduledIncome: yup.number().required()
      }),
      yup.object({
        scheduledInsurance: yup.number().required()
      }),
    ];

    const onSubmit = formData => alert(`入力結果をAPIに送信：\n${JSON.stringify(formData, null, 2)}`)

    return {
      validationSchema,
      onSubmit,
    };
  },
};
</script>

<style>
input,
select {
  margin: 10px 0;
  display: block;
}
</style>
