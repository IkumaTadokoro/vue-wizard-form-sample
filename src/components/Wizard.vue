<template>
  <div class="d-flex">
    <div class="d-flex-big">
      <h1>Step: {{ currentStep + 1 }}/8</h1>

      <Form @submit="nextStep" :validation-schema="currentSchema">
        <div class="form-group">
          <template v-if="currentStep === 0">
            <div class="form-flex-group">
              <div class="form-flex">
                <label for="name">Name</label>
                <Field name="name" id="name" v-model="formValues.name" />
                <ErrorMessage name="name" />
              </div>

              <div class="form-flex">
                <label for="email">Email</label>
                <Field
                    name="email"
                    id="email"
                    type="email"
                    v-model="formValues.email"
                />
                <ErrorMessage name="email" />
              </div>
            </div>
          </template>

          <template v-if="currentStep === 1">
            <div class="form-flex-group">
              <div class="form-flex">
                <label for="password">Password</label>
                <Field
                    name="password"
                    type="password"
                    id="password"
                    v-model="formValues.password"
                />
                <ErrorMessage name="password" />
              </div>

              <div class="form-flex">
                <label for="confirmation">Confirm Password</label>
                <Field
                    name="confirmPassword"
                    type="password"
                    id="confirmation"
                    v-model="formValues.password"
                />
                <ErrorMessage name="confirmPassword" />
              </div>
            </div>
          </template>

          <template v-if="currentStep === 2">
            <label for="address">Address</label>
            <Field
                as="textarea"
                name="address"
                id="address"
                v-model="formValues.address"
            />
            <ErrorMessage name="address" />

            <label for="postalCode">Postal Code</label>
            <Field
                name="postalCode"
                id="postalCode"
                v-model="formValues.postalCode"
            />
            <ErrorMessage name="postalCode" />
          </template>

          <template v-if="currentStep === 3">
            <label for="terms">Agree to terms and conditions</label>
            <Field
                name="terms"
                type="checkbox"
                id="terms"
                :value="true"
                v-model="formValues.terms"
            />
            <ErrorMessage name="terms" />
          </template>
        </div>

        <div class="button-group">
          <button v-if="currentStep !== 0" type="button" @click="prevStep">Previous</button>
          <button v-if="currentStep !== 3" type="submit">Next</button>
          <button v-if="currentStep === 3" type="submit" @click="showResult">Finish</button>
        </div>
      </Form>
    </div>

    <div class="d-flex-small">
      <h2>form-data-preview</h2>
      <pre><code>{{ formValues }}</code></pre>
    </div>
  </div>
</template>

<script>
import { Form, Field, ErrorMessage } from "vee-validate";
import * as yup from "yup";
import { ref, reactive, computed } from "vue";

export default {
  name: 'Wizard',
  components: {
    Form,
    Field,
    ErrorMessage,
  },
  setup: () => {
    const currentStep = ref(0)
    const formValues = reactive({})

    const schemas = [
      yup.object({
        name: yup.string().required(),
        email: yup.string().required().email(),
      }),
      yup.object({
        password: yup.string().required().min(6),
        confirmPassword: yup
            .string()
            .required()
            .min(6)
            .oneOf([yup.ref("password")], "Passwords must match"),
      }),
      yup.object({
        address: yup.string().required(),
        postalCode: yup
            .string()
            .required()
            .matches(/^[0-9]+$/, "Must be numeric"),
      }),
      yup.object({
        terms: yup.bool().required().equals([true]),
      }),
    ];

    const currentSchema = computed(() => {
      return schemas[currentStep.value];
    });

    const nextStep = (values) => {
      Object.assign(formValues, values)
      console.log("Current values: ")
      console.log(JSON.stringify(formValues, null, 2))
      currentStep.value++
    }

    const prevStep = () => {
      if (currentStep.value <= 0) {
        return
      }

      currentStep.value--
    }

    const showResult = () => {
      alert(Object.values(formValues).join(','))
    }

    return {
      currentStep,
      currentSchema,
      prevStep,
      formValues,
      nextStep,
      showResult
    }
  },
}
</script>

<style scoped>
.d-flex {
  display: flex;
  justify-content: center;
}

.d-flex-big {
  flex: 70;
}

.d-flex-small {
  flex: 30;
  border-left: 1px solid #2c3e50;
}

.button-group {
  margin-top:20px;
  display: flex;
  justify-content: space-around;
}

.form-flex-group {
  display: flex;
  flex-direction: column;
}

</style>
