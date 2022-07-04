<template>
  <div @click="$emit('click')">
     自定义事件
  </div>
</template>
<script>
export default {
  emits: ['click'] // 自定义事件只执行一次
}
</script>
<style scoped>

</style>
