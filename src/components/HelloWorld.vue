<template>
  <h1>{{ msg }}</h1>
  <Composition></Composition>
  <ModelButton></ModelButton>
  <Emits @click="onClick"></Emits>
  <comp></comp>
  <VmodelText v-model="counter"></VmodelText>
  <RenderTest v-model:counter="counter">
    <template v-slot:default>title</template>
    <template v-slot:content>Content...</template>
  </RenderTest>
  <Functional level="3">这是一个动态h元素</Functional>
  <p v-highlight="'green'">highlight this text!!!</p>
  <TransitionTest></TransitionTest>
  <button @click="sendMsg">emit event</button>
</template>

<script>
import {
  reactive,
  computed,
  onMounted ,
  onUnmounted,
  ref,
  toRefs,
  watch,
  h
} from 'vue'
import Composition from './Composition.vue'
import ModelButton from './ModelButton.vue'
import Emits from './Emits.vue'
import VmodelText from './VmodelText.vue'
import Functional from './Functional.vue'
import TransitionTest from './TransitionTest.vue'

// 事件的派发和监听
import mitt from 'mitt'
export const emitter = mitt()

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      counter: 1
    }
  },
  components: {
    Composition,
    ModelButton,
    Emits,
    VmodelText,
    RenderTest: {
      props: {
        counter: {
          type: Number,
          default: 0
        },
      },
      render() {
        const emit = this.$emit
        const counter = this.counter
        return h('div', [
          h("div", { onClick() {
            emit('update:counter', counter + 1)
          } }, [`I am RenderTest: ${counter}`, this.$slots.default(), this.$slots.content()])
        ])
      }
    },
    Functional,
    TransitionTest
  },
  methods: {
    onClick() {
      console.log("click me");
    },
    sendMsg() {
      emitter.emit('someEvent', 'fooo')
    }
  }
}
</script>
