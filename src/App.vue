<script setup>
import { ref } from 'vue';
import { Close } from '@element-plus/icons-vue'

let id = 0
const todosList = ref([])
const text = ref('')

const onAddTodo = () => {
  todosList.value.push({
    id: id++,
    text: text.value
  })
}

const onComplete = index => {
  todosList.value.splice(index, 1)
}

</script>

<template>
  <div class="todo-container">
    <h1>Todo List</h1>
    <div class="head">
      <el-input type="text" v-model="text"></el-input>
      <el-button @click="onAddTodo" type="primary">添 加</el-button>
    </div>
    <div class="list" v-if="todosList.length">
      <ul>
        <li v-for="(todo, index) in todosList" :key="todo.id">
          <span>{{ index + 1 }}. </span>
          <span>{{ todo.text }}</span>
          <el-icon :size="16" color="gray" @click="onComplete(index)" style="cursor: pointer;">
             <Close />
          </el-icon>
        </li>
      </ul>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.todo-container {
  margin: 50px auto 0;
  padding: 10px 10px 40px 10px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 600px;
  border: 1px solid #ddd;
  border-radius: 5px;
  box-shadow: 5px 5px 20px #333333;

  .head {
    display: flex;
    justify-content: space-evenly;
    align-items: center;
    width: 500px;
     .el-input {
      height: 40px;
     }
    .el-button {
      margin-left: 20px;
    }
  }

  .list {
    ul {
      list-style: none;
    }

    li {
      width: 500px;
      display: flex;
      align-items: center;
      line-height: 40px;
      margin: 5px 0;
    }
  }
}
</style>
