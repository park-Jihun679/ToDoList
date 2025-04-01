<script setup>
import { ref, onMounted, computed } from 'vue';
import HeaderLayout from './components/HeaderLayout.vue';
import InputContainer from './components/InputContainer.vue';
import TodoItem from './components/TodoItem.vue';

onMounted(() => {
  loadTodos();
});
const TITLE = '오늘의 할일';

const todos = ref([]);

const addTodo = (text) => {
  todos.value.push({
    id: Date.now(),
    text: text,
    createdAt: getFormatDate(),
    finishedAt: '',
  });
  saveTodos();
};

const removeTodo = (id) => {
  todos.value = todos.value.filter((todo) => todo.id !== id);
  saveTodos();
};

// localstrage 에 저장
const saveTodos = () => {
  localStorage.setItem('todos', JSON.stringify(todos.value));
};

// localstrage 에서 호출하는 함수
const loadTodos = () => {
  let list = localStorage.getItem('todos');
  list ? (todos.value = JSON.parse(list)) : [];
};

const getFormatDate = () => {
  const date = new Date();
  const nowMonth = date.getMonth() + 1;
  const nowDate = date.getDate();
  const nowHours = date.getHours();
  const nowMinutes = date.getMinutes();

  return nowMonth + '/' + nowDate + ' ' + nowHours + ':' + nowMinutes;
};
</script>

<template>
  <div class="container">
    <HeaderLayout :title="TITLE" />
    <TodoItem v-for="todo in todos" :todo="todo" @remove-todo="removeTodo" />
    <InputContainer @add-todo="addTodo" />
  </div>
</template>

<style scoped></style>
