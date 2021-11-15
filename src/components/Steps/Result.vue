<template>
  <div>
    <h2>確認</h2>
    <p>名前: {{ form.firstName }} {{ form.lastName }}</p>
    <p>Email: {{ form.Email }}</p>
    <p>電話番号: {{ form.tel }}</p>
    <p>誕生日: {{ form.birthday }}</p>
  </div>
</template>

<script>
export default {
  name: 'Result',
  props: {
    form: Object
  }
}
</script>

<style scoped>

</style>
