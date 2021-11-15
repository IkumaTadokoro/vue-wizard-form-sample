<template>
  <form @input="submit">
  <div class="form-group">
    <label for="Birthday">誕生日</label>
    <input type="date" class="form-control" v-model="birthday" placeholder="Enter Birthday">
  </div>
  </form>
</template>

<script>
export default {
  name: 'BirthdayForm',
  data() {
    return {
      birthday: null,
    }
  },
  methods: {
    submit() {
      this.$emit('update', {
        birthday: this.birthday
      })
    }
  }
}
</script>

<style scoped>

</style>
