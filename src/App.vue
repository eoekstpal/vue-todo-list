<!-- js -->
<script setup>
import { ref } from 'vue';

const inputValue = ref('');
const todoList = ref([{ text: 'vue', done:false}]);

console.log(inputValue.value);

const handleClickButton = () => {
  const text = inputValue.value;
  todoList.value.push({
    text: text, 
    done:false
  });
  console.log(todoList);
};

const handleChange = (event) => {
 const nextValue = event.target.value;
 inputValue.value = nextValue;
};

const handleClickDeleteButton = (index) => {
todoList.value.splice(index, 1);
}
</script>

<!-- html -->
<template>
  <p>{{todoList}}</p>
  <h1>ToDoList</h1>
<!--
  <input :value="inputValue" @change="handleChange"/>
-->
  <input v-model="inputValue" />
  <p>{{inputValue}}</p>
  <button @click="handleClickButton">확인</button>

  <div class="todo-item" v-for="(item, index) in todoList">
    <input type="checkbox" v-model=item.done />
    <span :class="{ 'done-item' : item.done}">{{ item.text }}</span>
    <button @click="">수정</button>
    <button @click="handleClickDeleteButton(index)">삭제</button>
  </div>

</template>

<!-- css -->
<style scoped>
.todo-item {
  width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  border: 1px solid yellow;
}
.done-item {
  text-decoration: line-through;
}
</style>
