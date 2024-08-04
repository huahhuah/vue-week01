<script setup>
import { ref } from 'vue'

const text = ref('這是一段文字')

const todos = ref([
  {
    id: 123,
    text: '12345'
  }
])
const tempEdit = ref({
  id: '',
  text: ''
})
const addTodo = () => {
  todos.value.push({
    text: text.value,
    id: new Date().getTime()
  })
  console.log(todos.value)
  text.value = ''
}
const deleteTodo = (todo) => {
  console.log(todo)
  const index = todos.value.findIndex((item) => item.id === todo.id)
  console.log(index)
  todos.value.splice(index, 1)
}
const prepareEdit = (todo) => {
  tempEdit.value = { ...todo } //拷貝
  //傳參考: 物件傳參考
  console.log(tempEdit.value)
  //tempEdit 的值,帶回去todos
}
const confirmEdit = () => {
  const index = todos.value.findIndex((item) => item.id === tempEdit.value.id)
  console.log(index, todos.value)
  //tempEdit的值帶回去todos
  todos.value[index] = tempEdit.value
  tempEdit.value = {}
}
</script>
<template>
  <div>
    <input type="text" v-model="text" />
    <button type="button" @click="addTodo">新增</button>
    <hr />

    <div v-for="todo in todos" :key="todo.id">
      {{ todo.text }}<button type="button" @click="deleteTodo(todo)">刪除</button>
      <button type="button" @click="prepareEdit(todo)">編輯</button>
      <hr />
    </div>
  </div>
  <div v-if="tempEdit.id">
    <h2>編輯區域</h2>
    當前修改的值: {{ tempEdit.text }}
    <br />
    <input type="text" v-model="tempEdit.text" />
    <button type="button" @click="confirmEdit">確認編輯</button>
    <button type="button" @click="tempEdit = {}">取消編輯</button>
  </div>
</template>
<style scoped>
* {
  margin: 0;
  padding: 0;
}
</style>
