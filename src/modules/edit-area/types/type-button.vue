<template>
  <van-button :style="ele.style" v-if="ele.config">
    {{ele.config[2].data}}
  </van-button>
</template>

<script>
export default {
  name: 'Button',
  props: {
    ele: Object
  }
}
</script>

<style scoped>
</style>

