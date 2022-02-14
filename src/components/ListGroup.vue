<template>
  <div class="listGroupTitle" v-if="title">{{title}}</div>
  <div v-loading="disabled" class="listGroupItem" :style="groupStyle?groupStyle:''">
    <slot />
  </div>
</template>
<script lang='ts' setup>
const props = defineProps({
  title: {
    type: String,
    default: ''
  },
  groupStyle: {
    type: String
  },
  disabled: {
    type: Boolean,
    default: false
  }
})
</script>
<style lang='sass' scoped>
@import '../styles/element/index.scss'
.listGroupItem
  overflow: hidden
  background-color: $--color-white
  margin: 20px
  padding: 0 0 0 0
  border-radius: 10px
  ::v-deep .listBorder:last-child
    display: none
.listGroupTitle
  margin: 20px 0 -15px 25px
  font-size: 18px
  color: $--color-black
</style>
