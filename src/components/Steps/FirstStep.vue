<template>
  <form @input="submit">
    <div class="form-group">
      <label for="firstName">姓</label>
      <input type="text" class="form-control" v-model="firstName" placeholder="Enter First Name">
    </div>
    <div class="form-group">
      <label for="lastName">名</label>
      <input type="text" class="form-control" v-model="lastName" placeholder="Enter Last Name">
    </div>
  </form>
</template>

<script>
export default {
  name: 'FirstStep',
  data() {
    return {
      firstName: null,
      lastName: null
    }
  },
  methods: {
    submit() {
      this.$emit('update', {
        firstName: this.firstName,
        lastName: this.lastName
      })
    }
  }
}
</script>

<style scoped>

</style>
