<template>
  <h1>Step: {{ stepNumber }}</h1>
</template>

<script>
export default {
  name: 'FirstStep',
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
  }
}
</script>

<style scoped>

</style>
