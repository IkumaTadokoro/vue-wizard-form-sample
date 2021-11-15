<template>
  <div class="d-flex">
    <div class="d-flex-big">
      <h1>Step: {{ stepNumber }}</h1>
      <FirstStep v-if="stepNumber === 1" @update="updateForm"></FirstStep>
    </div>

    <div class="d-flex-small">
      <h2>form-data-preview</h2>
      <pre><code>{{ form }}</code></pre>
    </div>
  </div>
</template>

<script>
import FirstStep from '@/components/Steps/FirstStep'

export default {
  name: 'Wizard',
  components: {
    FirstStep
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


</style>
