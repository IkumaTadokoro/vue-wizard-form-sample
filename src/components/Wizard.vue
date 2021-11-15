<template>
  <div class="d-flex">
    <div class="d-flex-big">
      <h1>Step: {{ stepNumber }}</h1>
      <FirstStep v-if="stepNumber === 1" @update="updateForm"></FirstStep>
      <ContactForm v-if="stepNumber === 2" @update="updateForm"></ContactForm>
      <BirthdayForm v-if="stepNumber === 3" @update="updateForm"></BirthdayForm>
      <Result v-if="stepNumber === 4" :form="form"></Result>

      <div class="button-group">
        <button @click="backStep" v-show="stepNumber !== 1">まえの質問へ</button>
        <button @click="nextStep" v-show="stepNumber !== 4">つぎの質問へ</button>
        <button @click="showData" v-show="stepNumber === 4">計算結果へ</button>
      </div>
    </div>

    <div class="d-flex-small">
      <h2>form-data-preview</h2>
      <pre><code>{{ form }}</code></pre>
    </div>
  </div>
</template>

<script>
import FirstStep from '@/components/Steps/FirstStep'
import ContactForm from '@/components/Steps/ContactForm'
import BirthdayForm from '@/components/Steps/BirthdayForm'
import Result from '@/components/Steps/Result'

export default {
  name: 'Wizard',
  components: {
    FirstStep,
    ContactForm,
    BirthdayForm,
    Result
  },
  data() {
    return {
      stepNumber: 1,
      form: {
        firstName: null,
        lastName: null,
        Email: null,
        tel: null,
        birthday: null
      }
    }
  },
  methods: {
    updateForm(formData) {
      // [Object.assign()](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)
      Object.assign(this.form, formData)
    },
    backStep() {
      this.stepNumber--;
    },
    nextStep() {
      this.stepNumber++;
    },
    showData() {
      alert(`入力結果：${Object.values(this.form).join(',')}`)
    }
  }
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

</style>
