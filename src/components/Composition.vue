<template>
  <div>
    <p>{{counter}}</p>
    <p>{{doubleCounter}}</p>
    <p ref="desc"></p>
  </div>
</template>
<script>
import { reactive, computed, onMounted , onUnmounted, ref, toRefs, watch} from 'vue'
export default {
  name: 'Composition',
  setup() {
    // counter相关
    const {counter, doubleCounter} = useCounter()

    // 其他数据，单值响应式
     const msgs = ref('some message')

     // 使用元素引用
     const desc = ref(null)

     // 侦听器
     watch(counter, (val, oldval) => {
       const p = desc.value
       p.textContent = `counter change from ${oldval} to ${val}`
     })
    
    return {counter, doubleCounter, msgs, desc}
  }
}
function useCounter() {
  const data = reactive({
    counter: 1,
    doubleCounter: computed(() => data.counter * 2)
  })
  let timer
  onMounted(() => {
    timer = setInterval(() => {
      data.counter++
    }, 1000);
  })
  onUnmounted(() => {
    clearInterval(timer)
  })
  return toRefs(data)
}
</script>
<style scoped>

</style>
