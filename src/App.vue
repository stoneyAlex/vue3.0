<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <!-- <HelloWorld msg="Hello Vue 3.0 + Vite" /> -->
  <Todo></Todo>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Todo from './components/todos/Todo.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    Todo,
  }
}
</script>
