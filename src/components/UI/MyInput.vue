<template>
 <input :value="value" @input="changeValue" type="text" class="input"/>
</template>

<script>
export default {
  name: 'my-input',
  props: {
    value: [String, Number]
  },
  methods: {
    changeValue(e) {
      this.$emit('update:value', e.target.value)
    }
  }
}

</script>

<style scoped>
.input {
  margin-top: 10px;
  height: 35px;
}
</style>