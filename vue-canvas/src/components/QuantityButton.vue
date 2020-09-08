<template>
  <input type="submit" :value="msg" @click="render()">
</template>

<script>
export default {
  name: 'QuantityButton',
  props: {
    msg: String
  },
  methods: {
    render() {
      this.$root.$emit('render');
    }
  }
}
</script>