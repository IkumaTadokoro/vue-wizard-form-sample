<template>
  <form @input="submit">
    <div class="form-group">
      <label for="Email">Eメール</label>
      <input type="text" class="form-control" v-model="Email" placeholder="Enter Email">
    </div>
    <div class="form-group">
      <label for="tel">電話番号</label>
      <input type="text" class="form-control" v-model="tel" placeholder="Enter Tel">
    </div>
  </form>
</template>

<script>
export default {
  name: 'ContactForm',
  data() {
    return {
      Email: null,
      tel: null
    }
  },
  methods: {
    submit() {
      this.$emit('update', {
        Email: this.Email,
        tel: this.tel
      })
    }
  }
}
</script>

<style scoped>

</style>
