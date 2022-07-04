<template>
  <div>
    <button @click = "show = !show">Toggle</button>
    <transition name="fade">
      <p v-if="show">hello</p>
    </transition>
  </div>
</template>
<script>
import {emitter} from './HelloWorld.vue'
export default {
  data() {
    return {
      show: true
    }
  },
  mounted() {
    emitter.on('someEvent', masg => {
      console.log('msg')
    })
  }
}
</script>
<style scoped>
  .fade-enter-active,
  .fade-leave-active {
    transition: opacity 0.5s ease;
  }
  .fade-enter-from,
  .fade-leave-to {
    opacity: 0;
  }
</style>
