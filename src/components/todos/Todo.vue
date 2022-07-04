<template>
  <div>
    <EditTodo
      v-model:todo-title="newTodo"
      @keyup.enter="addTodo"
      autofocus
      placeholder="新增今日代办"
      autocomplete="off"
    ></EditTodo>
    <ul>
      <TodoItem
        v-for="todo in filterdTodos"
        :key="todo.id"
        :todo="todo"
        v-model:edited-todo="editedTodo"
        @remove-todo="removeTodo"
      ></TodoItem>
    </ul>
    <Filter :items="filterItems" v-model="visibility"></Filter>
  </div>
</template>
<script>
import { reactive, toRefs } from 'vue'
import TodoItem from './TodoItem.vue'
import Filter from './Filter.vue'
import {useTodos} from './useTodos.js'
import {useFilter} from './useFilter.js'

export default {
  components: {
    TodoItem,
    Filter
  },
  setup() {
    const todoState = reactive({
      newTodo: '',
      editedTodo: null,
    })
    const {todos, removeTodo, addTodo} = useTodos(todoState)
    const filterState = useFilter(todos)

    return {
      ...toRefs(todoState),
      ...toRefs(filterState),
      addTodo,
      removeTodo,
    }
  },
}
</script>
<style scoped>

</style>
