<template>
  <select @change="selectChange" :value="chosenOption">
    <option disabled value="">Choose option ...</option>
    <option
        v-for="option in options"
        :key="option.value"
        :value="option.value"
    >
      {{ option.title }}
    </option>
  </select>
</template>

<script>
export default {
  name: 'my-select',
  props: {
    chosenOption: {
      type: String
    },
    options: {
      type: Array,
      default: () => [],
      required: true
    }
  },
  methods: {
    selectChange(e) {
      this.$emit('update:chosenOption', e.target.value)
    }
  }
}
</script>

<style scoped>

</style>