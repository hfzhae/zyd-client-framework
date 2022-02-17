<template>
  <div class="blockGroupTitle" v-if="title">{{title}}</div>
  <div class="blockGroupItem">
    <slot />
  </div>
</template>
<script lang='ts' setup>
const props = defineProps({
  title: {
    type: String,
    default: ''
  },
  groupClass: {
    type: String
  },
  disabled: {
    type: Boolean,
    default: false
  }
})
</script>
<style lang='sass' scoped>
.blockGroupItem
  overflow: hidden
  display: flex
  flex-wrap: wrap
  margin: 10px 20px
  border-radius: 10px
.blockGroupTitle
  margin: 20px 0 -0px 25px
  font-size: 18px
  color: #000000
</style>